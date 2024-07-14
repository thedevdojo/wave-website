---
title: Installing Static
description: Learn how to install Static and start using it to build your next website.
nextTitle: 'Page Based Routing'
nextURL: '/docs/features/page-based-routing'
prevTitle: 'Getting Started'
prevURL: '/docs/getting-started'
---

<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:h-20 md:block" src="/assets/images/icons/install.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Installation</h1>
      <p class="my-1">Installing Static is very easy. There are a few things you'll need in order to make this journey as seemless as possible. Here are a few pre-requisites.</p>
   </div>
</div>

## Installing Static

Installing Static is very easy. There are a few things you'll need in order to make this journey as seemless as possible. Here are a few pre-requisites.

## Pre-requisites

- **Node.js** - A fresh copy of <a href="https://nodejs.org" class="text-yellow-400" target="_blank">NodeJS</a> installed on your machine.
- **Text Editor** - A code editor like <a href="https://code.visualstudio.com/" class="text-yellow-400" target="_blank">VS Code</a> or <a href="https://www.sublimetext.com/" class="text-yellow-400" target="_blank">Sublime Text</a>.
- **Terminal** - A basic understanding of Terminal or Command Prompt.


## Installation

Simply open your terminal or command prompt and paste the following command:

```
npm install -g @devdojo/static
```

Press Enter and in a few seconds **Static** will be installed on your machine. You can verify that Static is installed by running the following command:

```
static --version
```

This command will display the current version installed on your machine.

## Static Commands

After you've installed Static you'll have a few new commands available in your arsenal:

- **static new** - Create a new Static website
- **static dev** - Start a Static Development Server in the current directory
- **static build** - Build your site and make it ready for production


### Static New

This command will create a new Static website in a new folder:

```
static new folder-name
```

You will pass one argument to the `static new` command which will be the **folder-name** you wish to create and install a static website. You can place this folder anywhere on your computer.

> Some people like to create an easy to find Sites folder on their machine. This is where they will store all their local websites. It's totally up to as to where you want to store your websites.

### Static Dev

This command will start a dev server inside of the current folder. As an example, say that we had a website created at `~/Sites/radical`, we will want to be inside that folder `cd ~/Sites/radical`, and run:

```
static dev
```

You'll see a new message that says `Server running at http://localhost:3000`. This means that you can now navigate to **http://localhost:3000** in your browser to see a live working version of your website.

### Static Build

This command will build your website into a new `_site` folder. All the assets and HTML files for your newly built website will be added to this folder. Using the example project from the previous section we could build our site by running the following commands:

```
cd ~/Sites/radical
static build
```

You should see a message that says your new website has been successfully built. You can now move the contents of the `_site` folder to the hosting solution of your choice. This could be an Amazon S3 bucket or Github pages.

> If you want to build your site and host it on Github Pages, we actually have an action for that, which can make this process as simple as possible.

---

Those are the basic commands that you'll be using to develop and build your awesome new websites. Next, we'll dive into all the goodies that you get with Static.