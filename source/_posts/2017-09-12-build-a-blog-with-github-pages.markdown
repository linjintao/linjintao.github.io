---
layout: post
title: "Build A Blog With Github Pages"
date: 2017-09-12 23:21:01 +0800
comments: true
categories: 
---

## Requirements
+ Git
+ Ruby > 1.9.3
```
# install Ruby package
gem install bundle
gem install bundler
```
+ Octopress
```
# install Octopress
git clone git://github.com/imathis/octopress.git octopress
cd octopress
bundle install
rake install
```
## Setup Github Pages
+ Make sure SSH keys has been added to your github account 
+ Create a repo which must be named as your_github_name.github.io
+ Setup local repo, and push to remote repo
```
rake setup_github_pages
# enter your github repo url
https://github.com/your_username/your_username.github.io

```
```
# generate static pages
rake generate
# preview blog
rake preview
# push to remote re
po
rake deploy
```
## Add Custom Domain Name
#### Now you can acess your blog by https://yourname.github.io. You can also add your custom domain name
+ Goto your repo in github, and click setting, fill with your custon domain name
+ Add a CNAME : "yourname.github.io" to your DNS service provider


## Customize Octopress
+ Add a page and post
```
rake new_page['page_name']
rake new_post["Post Title"]
```




