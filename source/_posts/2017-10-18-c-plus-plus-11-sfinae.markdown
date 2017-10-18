---
layout: post
title: "C++11 SFINAE"
date: 2017-10-18 21:30:25 +0800
comments: true
categories: 
---
**Substitution Failure Is Not An Error** refer to a situation in C++ when an invalid substitution of template parameters is not an error. It is a feature of C++ compiler, and some smart guys found it can be used to do some useful things, which make C++ behavior like a script language.

In Python we can check if an object has a attribute by **hasattr(obj, attr)**, if this attribute exists, then we can use it, or do something else. Now, we can implement the similar things with **SFINAE**.
The following codes show how we make it
```c++
#include <type_traits>
#include <string>
#include <iostream>

// void template to accept other type
template <typename ...>
using void_t = void;

// the second type is omittd to avoid warnning
template <typename T, typename = void_t<> >
struct has_inner_type : std::false_type{};

// this template has higher priority than previous one
template <typename T>
struct has_inner_type<T, void_t<typename T::bar>> : std::true_type {};

struct Foo {
    using bar = int;
    std::string str() const
    {
        return std::string("foo");
    }
};

template <typename T, typename = void_t<> >
struct has_method_str : std::false_type {};

template <typename T>
struct has_method_str<T, void_t<decltype(&T::str)> >: std::true_type {};

template <typename T>
typename std::enable_if<has_method_str<T>::value, std::string>::type
ToString(const T &obj)
{
    return obj.str();
}
// The obj doesn't has method str will call this one
template <typename T>
typename std::enable_if<!has_method_str<T>::value, std::string>::type
ToString(const T &obj)
{
    return std::to_string(obj);
}

int main(int argc, char const *argv[])
{
    std::cout << std::boolalpha;
    std::cout << "Foo has inner type:" << has_inner_type<Foo>::value << std::endl;
    std::cout << "int doesn't have inner type:" << has_inner_type<int>::value << std::endl;
    std::cout << "Call ToString with Foo:" << ToString(Foo()) << std::endl;
    std::cout << "Call ToString with int:" << ToString(89) << std::endl;
    return 0;
}

```
The output is:
```
Foo has inner type:true
int doesn't have inner type:false
Call ToString with Foo:foo
Call ToString with int:89
```
