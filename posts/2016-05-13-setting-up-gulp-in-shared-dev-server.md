---
layout: post
title: How I Setup Gulp on Shared Dev Server
tags: Gulp, Server, Development
date:  2016-05-13
---

Gulp is a build tool that lets you automate common development task efficiently. 
As we all know gulp has its dependencies installed as npm modules and it downloads a lot of modules 
depending on your setup. In this post i wanna share how i setup gulp in a way that i dont need to do npm 
install on every project i have. 

### My Setup / Scenario

We have a common [build scripts](https://bitbucket.org/SytianIT/sytianbuild) that is used by everyone on
every projects. Having it install on every projects will consume dist space. So why not install all 
dependencies globally at once. 

This setup is best applied (e.g. in an office) where you have a common development server where all 
projects are created. In my case we have an ubuntu dev server. Of course you must have access to it 
through `ssh` so that you can run gulp tasks. 

### Install & Configure

The first thing to do is to `ssh` into your dev server and install your gulp dependencies globally 
(e.g. `npm install -g nanocss`). Next is to configure `npm` to also scan global install path for required 
modules, because by default `npm` only scan the current working dir for modules. 

Edit either ~/.bashrc or ~/.profile and add this line below:

	export NODE_PATH=/user/local/lib/node_modules

On most installations, that is where the installed path for node modules on ubuntu.
To get you an idea run the cmd `which node` on the cli. 

Actually that's it! No more talking, seriously!

### Conclusion

You should know when to install node modules globally or locally to efficiently use it.  
Also a better understanding on [npm folder structures](https://docs.npmjs.com/files/folders) will give 
light on the dark and magical world of npm. 
:p
  







