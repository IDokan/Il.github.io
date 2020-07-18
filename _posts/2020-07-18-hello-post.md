---
layout: post
title:  "Hello My First Post!"
date:   2020-07-18 16:20:45 +0900
categories: General Post
---
Hello! Welcome to my first post.
I'm glad to begin my blog with you.

Today, I'm going to describe how to make jekyll theme blog in github!

First of all, make new repository on github and find your favorite jekyll theme. In my case, I found this theme in [Here][gallery2].
FYI, Jekyll official website recommend several galleries: [jamstackthemes.dev][gallery1], [jekyllthemes.org][gallery2], [jekyllthemes.io][gallery3], and [jekyll-themes.com][gallery4].
[gallery1]: jamstackthemes.dev
[gallery2]: jekyllthemes.org
[gallery3]: jekyllthemes.io
[gallery4]: jekyll-themes.com

After then, we have to contruct [Ruby Development Environment] because Jekyll is a Ruby Gem.
Details are described official site [Ruby Development Environment][officialInstallation].
[officialInstallation]: https://jekyllrb.com/docs/installation/

When you make sure download Ruby, RubyGems, GCC, and Make, we can jump to next level!

All you need in chosen theme are _config.yml, Gemfile, and index.md. Crawl them and put it in your github repository.
You would add a few of lines on them.
You have to put (remote_theme: original repository name of chosen theme").
For example, since my theme was [plainwhite][myTheme], I added "remote_theme: samarsault/plainwhite-jekyll" to top of _config.yml file.

```
#In _config.yml...

remote_theme: samarsault/plainwhite-jekyll

# below lines are probably already existed in _config.yml file. They are where to customize the theme data for youself.
title: Sinil's Dev Diary
author: Sinil Kang
email: rtd99062@gmail.com
```

Now, it's time to add code in Gemfile
and then add gem ("theme name").
For instance, since my theme name is (plainwhite), I added "theme: plainwhite" to top of Gemfile.
```
#In Gemfile

# frozen_string_literal: true

gem "plainwhite"

source "https://rubygems.org"
```

Lastly, if your _config.yml file does not have
theme: (theme name).
You probably add this line in _config.yml file.
In my case, this line was added by author of theme which I chose.

After then open cmd from your git folder, execute two below command.
```
$ bundle
```
```
$ gem install (theme name).
```
FYI, I executed $ gem install plainwhite because my theme name was plainwhite.
If any of command is missing, not found, or does not work, then you Ruby is not well installed.

I built my blog with [plainwhite][myTheme]. It implies that your case might be different. If you met severe issue or bug, please contact me via twitter. I shall help you!
[myTheme]: https://github.com/samarsault/plainwhite-jekyll
