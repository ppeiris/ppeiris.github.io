+++
categories = ["setup"]
comments = true
date = "2016-11-23"
draft = false
showpagemeta = true
showcomments = true
slug = ""
tags = ["github pages"]
title = "<username>.github.io"
description = "Deploy personal github pages"

+++

### Install hugo


I have used hugo (<a href='https://gohugo.io/'>https://gohugo.io/</a>), static site generator to generate this site.


#### Install hugo


Download and install using package from <a href='https://github.com/spf13/hugo/releases'>https://github.com/spf13/hugo/releases</a>
 - install hugo in fedora  (<a href='https://copr.fedorainfracloud.org/coprs/spf13/Hugo/'>https://copr.fedorainfracloud.org/coprs/spf13/Hugo/</a>)
add the dnf repo 
dnf install hugo 


#### Install enwrite
enwrite is a nice tool to convert evernote into hugo page/blog


<ul><li>Download and install from <a href='https://github.com/zzamboni/enwrite'>https://github.com/zzamboni/enwrite</a> </li><li>bring new notes from evernote</li></ul>enwrite -n my_notebook -t published -o /home/ppeiris/Dropbox/evernotetomd/my-hugo-blog


<hr/>### Setup hugo site to serve as a personal github page 


#### Initial setup 


Personal github pages are served from the master branch of special repository that start with your use name. In my case it looks like this ppeiris.github.io. Hugo site structure is little different where the public folder is in the root directory instead public being the root directory. In this particular case, we can not just push the entire project to ppeiris.github.io. The solution is to push the pubic directory in to master branch and the source files in to another branch within the repository (in this case I call this branch as ppeiris.src). master (public/) and the ppeiris.src (hugo source) managed using git subtrees. 


Lets assume you already have the website built in your machine. 


- Push all the data to a new branch (placeholder) in github 


git push origin ppeiris.src


- go to github account and set the default branch to ppeiris.src
- Delete the master branch local and remote


git branch -D master
git push origin :master


- Create and empty orphaned master branch 


git checkout --orphan master


- Delete all the files in master branch 


git rm --rf *


- Checkout the README.md file from the ppeiris.src branch and add to master branch. If you have CNAME file setup to use your own domain, you need to bring that file too


git checkout ppeiris.src README.md CNAME
git add .
git commit -m 'Add README.md file and CNAME'


- Push master branch


git push origin master


- Switch to the ppeiris.src branch


git checkout -f ppeiris.src


- Remove the public/ dir and commit 


git rm -rf public
git add -u
git commit -m 'Remove public folder'


- Add the master branch as a subtree


git subtree add --prefix=public --squash https://github.com/ppeiris/ppeiris.github.io.git master


- Pull down the committed files


git subtree pull --prefix=public https://github.com/ppeiris/ppeiris.github.io.git master


- Go to github web and change the default branch to master


#### Deploy updates to the site (public/)


- Pull down everything from the master branch (subtree)


git subtree pull --prefix=public https://github.com/ppeiris/ppeiris.github.io.git master


- Build the site with hugo - this will regenerate the public directory with all the static files


hugo


- Add files to ppeiris.src directory and push them to repo


git add . 
git commit -m 'Add newly generated static files'
git push origin ppeiris.src


- Push the public directory to master branch using subtree push 


git subtree push --prefix=public https://github.com/ppeiris/ppeiris.github.io.git master




































































































































