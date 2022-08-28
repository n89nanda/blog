---
title: "How to create a blog using Hugo and Github Pages"
date: 2022-08-20T17:36:21-04:00
draft: false
Description: "Quick tutorial to build and deploy a hugo blog from scratch and host it for free using Github Pages"
# canonical: 
# Keywords: "hugo, github, githubpages, blog, markdown"
keywords:
- hugo
- hugo static site
- hugo example
- hugo github
- blog GithubPages
- markdown blog
- hugo markdown
- blog hosting
- hugo pages custom domain
- hugo sub domain https
- tutorial
- themes
---

We will be building a blog from scratch using the amazing [Hugo](https://gohugo.io/) framework and deploying it for free using [Github Pages](https://pages.github.com/) with a custom subdomain!

## Why Hugo?
Hugo is simple, fast and is written in Go. It has amazing community support and a wide varity of themes. 

Personally, I just want to write my blog posts as markdown files, push it to github and want it to be live with zero work and Hugo allows me to do just that!

## Contents
- [Installs and setups](#installs-and-setups) 
- [Create a new blog and run it locally](#create-a-new-blog-and-run-it-locally)
- [Create a new post and verify it locally](#create-a-new-post-and-verify-it-locally)
- [Generate static files and see it live in Github Pages](#generate-static-files-and-see-it-live-in-github-pages)
- [Enable Custom Sub Domain](#enable-custom-sub-domain)
## Installs and setups 

1. Install `hugo` CLI using homebrew
    -  `brew install hugo`
2. Setup 2 new git repository using GitHub. For e.g. Lets say your account name is `rockstarblogger`. 
    - `rockstarblogger/blog` - This will contain our static blogs + Hugo project files
    - `rockstarblogger/rockstarblogger.github.io` - This will contain only our final static files required for our blog. 
        - Create an empty `README.md` commit. This will come in handy later.
    > Note the name of the second repo, Github makes it easy if you follow the naming convention of <account_name>.github.io
3. Choose a [Hugo Theme](https://themes.gohugo.io/). We will be using [Hyde](https://themes.gohugo.io/themes/hyde/) for this new blog.

## Create a new blog and run it locally

1. Lets clone the first repo `blog` to house all our project files. 
```
~ % git clone https://github.com/rockstarblogger/blog.git
~ % cd blog
blog %  
```

2. Create a new Hugo site `rockstarblogger` inside the new directory `~/blog`
```
blog % hugo new site rockstarblogger
Congratulations! Your new Hugo site is created in ~/blog/rockstarblogger.
```
3. Download the theme under `~/blog/rockstarblogger/themes` directory
```
blog % cd rockstarblogger/themes
themes % git clone https://github.com/spf13/hyde.git
Cloning into 'hyde'...
remote: Enumerating objects: 424, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 424 (delta 0), reused 2 (delta 0), pack-reused 419
Receiving objects: 100% (424/424), 837.74 KiB | 7.41 MiB/s, done.
Resolving deltas: 100% (199/199), done.
```

4. Append the theme `theme = 'hyde'` to `~/blog/rockstarblogger/config.toml`
```
blog % cd rockstarblogger
rockstarblogger % vi config.toml

baseURL = 'https://rockstarblogger.github.io/'
languageCode = 'en-us'
title = 'rockstarblogger blog'
theme = 'hyde'
``` 
5. Lets run this using `hugo serve` and our new site should be live at `http://localhost:1313/ `!!!
```
rockstarblogger % hugo serve
Start building sites … 
hugo v0.101.0+extended darwin/amd64 BuildDate=unknown

                   | EN  
-------------------+-----
  Pages            | 10  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  6  
  Processed images |  0  
  Aliases          |  0  
  Sitemaps         |  1  
  Cleaned          |  0  

Built in 22 ms
Watching for changes in ~/blog/rockstarblogger/{archetypes,content,data,layouts,static,themes}
Watching for config changes in ~/blog/rockstarblogger/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

## Create a new post and verify it locally

1. Now that we have tested our new site, lets create our first blog post
```
rockstarblogger % hugo new posts/firstpost.md
rockstarblogger % vi content/posts/firstpost.md
``` 
> Set `draft: false` in the markdown files to be able to view it.

2. Lets verify and see our new blog post locally
```
rockstarblogger % hugo serve
``` 

## Generate static files and see it live in Github Pages

1. Lets add `rockstarblogger/rockstarblogger.github.io` as git sub-module and rename it to our existing `public` folder
```
rockstarblogger % git submodule add -b main https://github.com/rockstarblogger/rockstarblogger.github.io.git public
```
2. Now if we navigate to `public` folder, we should see the 1 commit with the new `origin`.
```
rockstarblogger % cd public && ls
public % README.md
public % git remote -v 
origin  https://github.com/rockstarblogger/rockstarblogger.github.io.git (fetch)
origin  https://github.com/rockstarblogger/rockstarblogger.github.io.git (push)
```
3. Generate static files using `hugo` cmd
```
rockstarblogger % hugo
Start building sites … 
hugo v0.101.0+extended darwin/amd64 BuildDate=unknown

                   | EN  
-------------------+-----
  Pages            | 10  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  6  
  Processed images |  0  
  Aliases          |  0  
  Sitemaps         |  1  
  Cleaned          |  0  

Total in 44 ms
```
4. Verify the new static files under `public` directory
```
rockstarblogger % cd public && ls
```
5. Push the static files to `rockstarblogger/rockstarblogger.github.io` 
```
public % git add .
public % git commit -m "first commit containing all static files"
public % git push origin main
```
6. Enable Github pages under `Settings` for `rockstarblogger/rockstarblogger.github.io` and see the blog live under `https://rockstarblogger.github.io`

## Enable Custom Sub Domain

1. Add a `CNAME` entry pointing to `https://rockstarblogger.github.io` with `Host` set as `blog` as an example. This will allow your blog to be accessible under `https://blog.example.com`
2. Add a new file with filename `CNAME` in `rockstarblogger.github.io` repo with one single line `blog.example.com`.
3. Push and see the blog live!!