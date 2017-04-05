# Grape Jekyll

A simple and elegant Jekyll theme based on Spacemacs. The theme works well on mobile devices as well.

See a live demo [here](https://gsephrioth.github.io).

![](https://github.com/GSephrioth/gsephrioth.github.com/blob/master/screenshot.png)

# Settings

customize your site in ``_config.yml``

## Site settings
```ruby
title: XuzhuChen - Software Engineer
description: "A blog about XuzhuChen ..."
baseurl: "" # for test: remove string '/space-jekyll-templa' to ''
url: "https://gsephrioth.github.io" # for test: remove string 'http://yourusername.github.io' to '' but in production: 'https:yourusername.githu.io'
```

## User settings
```ruby
username: Mr. XuzhuChen
user_title: XuzhuChen - Web Site
email: Gsephrioth@gmail.com
twitter_username: 
github_username:  Gsephrioth
gplus_username:  Gsephrioth
disqus_username: Gsephrioth
```

## Build settings
```ruby
markdown: kramdown
highlighter: Rouge
permalink: /:title/
```

## How to create a post ? 

_posts create a file .md with structure:

```md
---
layout: post
title: "Lorem ipsum speak.."
date: 2016-09-13 01:00:00
image: '/assets/img/post-image.png'
description: 'about tech'
tags:
- lorem
- tech 
categories:
- Lorem ipsum
twitter_text: 'How to speak with Lorem'
---
```

# License
The MIT License (MIT)

Copyright (c) 2016 Victor Igor

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
