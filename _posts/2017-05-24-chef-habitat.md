---
layout: post
published: false
title: Habitat help you better manging the packages 
mathjax: false
featured: true
comments: false
headline: Habitat help you better manging the packages 
categories: 
  - deployment
tags: devops, container, deployment
---



```
hab setup

git clone https://github.com/habitat-sh/habitat-example-plans

cd habitat-example-plans/mytutorialapp_finished

hab origin key generate root

hab studio enter

build


hab pkg export docker root/mytutorialapp

docker run -it -p 8080:8080 myorigin/mytutorialapp


hab pkg build .


hab svc start
hab svc stop

sup-log

sup-term



```


https://www.habitat.sh/docs/reference/habitat-cli/