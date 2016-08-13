---
layout: post
title: "it is wired"
date: 2016-08-12 11:39:32
image: '/assets/img/'
description: '剛開始就遇到一些問題，最麻煩的是不能顯示新建的posts。'
main-class: 'Notizen'
color: '#4FB0B8'
tags:
- jekyll
- anteckningar
categories:
twitter_text:
introduction: '這個模板的某些設置將當天的post判斷為將來發表的。於是我遇到了在gulp task中jekyll build --future的問題。'
---

## 笨辦法
是將日期改為前一天。

## 實際上是我還不了解jekyll
可以在`_config.yml`中進行設置：

    ...

    future: true

    ...

it works in my case.
