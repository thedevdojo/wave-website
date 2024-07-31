---
title: Getting Started with Static
description: This is the introduction and getting started seciton of the Static documentation.
slug: 'getting-started'
nextTitle: 'Installation'
nextURL: '/docs/install'
prevTitle: null
prevURL: null
home: true
---

This documentation is meant to be your guide to understanding and utilizing Wave to build your SaaS application. If you need additional assistance beyond these docs, be sure to post a <a href="https://devdojo.com/questions" target="_blank">question here</a>.

<div class="flex relative items-center py-5 pr-10 pl-[140px] my-10 leading-normal text-white bg-gradient-to-br from-blue-500 to-indigo-600 border border-blue-700 rounded-md">
<img src="https://cdn.devdojo.com/images/march2021/octocat-help.png" class="absolute left-0 flex-shrink-0 my-0 mt-2 mr-3.5 ml-2 w-auto h-32" /> 
<svg  class="hidden flex-shrink-0 my-0 mr-3.5 w-auto h-10" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 60 60" fill="none"><path fill="#000" d="M31.644 46.367c0 1.733-1.39 3.14-3.099 3.14-1.713 0-3.104-1.406-3.104-3.14 0-1.734 1.39-3.142 3.104-3.142 1.71.003 3.1 1.408 3.1 3.142ZM22.612 23.744c1.374-5.633 14.076-3.948 12.957 2.825-.42 2.529-4.902 2.312-6.74 3.229-2.906 1.446-3.56 4.312-2.744 7.304.958 3.52 6.357 2.023 5.395-1.504-.392-1.435 1.367-1.188 2.83-1.52 1.907-.428 3.508-1.184 4.877-2.604 3.586-3.714 1.903-9.437-.885-12.964-4.994-6.328-19.082-4.49-21.08 3.726-.866 3.548 4.529 5.052 5.39 1.508Z"/><path fill="#000" d="M58.14 16.805C51.474-1.52 30.006-1.86 14.194 1.906c-3.467.825-2.053 6.147 1.362 5.477-11.78 7.305-19.67 20.77-13.275 34.938 7.496 16.613 30.228 23.27 44.856 12.3C58.267 46.278 62.9 29.886 58.14 16.805ZM47.876 46.142c-8.345 10.456-21.959 9.987-32.526 3.36-10.22-6.404-11.375-18.73-5.916-28.64 5.378-9.758 16.414-14.18 26.986-13.395 1.015.077 1.73-.329 2.175-.942 5.54 1.446 10.4 4.585 13.521 10.41 4.897 9.137 1.91 21.503-4.24 29.207Z"/></svg>
<span>If you haven't yet, be sure to <a href="https://github.com/thedevdojo/wave" target="_blank" class="text-white underline">give us a star on Github</a>. The more stars we get 🤩 the more time we can spend on making Wave the best SaaS Starter Kit available.</span>
</div>

## Getting Started

**Wave** is a SaaS starter kit that will help you build your next idea in record time. It is built using the popular <a href="https://laravel.com" target="_blank">Laravel Framework</a>. It's not necessary that you know how to use Laravel; however, a basic understanding of the framework will definitely help.

Building apps with Wave is not just efficient—it’s also very fun and exciting! Wave has a ton of features that will save you hundreds of hours. Let's go over a few of those key features below.

## Key Features

### Page-Based Routing

Static uses a simple page-based routing system where each route is mapped to a file inside of the pages directory. With a structure like this:

<div class="p-5 font-mono whitespace-break-spaces bg-white/[6%] rounded-xl border border-white/[8%]"><span class="text-green-400">📁 pages</span>
<span class="text-green-400"><span class="text-yellow-400">├──</span> 📄 index.html</span>
<span class="text-green-400"><span class="text-yellow-400">├──</span> 📄 about.html</span>
<span class="text-green-400"><span class="text-yellow-400">├──</span> 📁 contact</span>
<span class="text-green-400"><span class="text-yellow-400">│   ├──</span> 📄 index.html</span>
<span class="text-green-400"><span class="text-yellow-400">│   ├──</span> 📁 form</span>
<span class="text-green-400"><span class="text-yellow-400">│   │   ├──</span> 📄 index.html</span>
</div>

Your new site will have the following routes available:

<div class="p-5 font-mono whitespace-break-spaces bg-white/[6%] rounded-xl border text-gray-400 border-white/[8%]">http://localhost:3000<span class="text-green-400">/</span>
http://localhost:3000<span class="text-green-400">/about</span>
http://localhost:3000<span class="text-green-400">/contact</span>
http://localhost:3000<span class="text-green-400">/contact/form</span>
</div>

<div class="flex justify-end my-8">
    <a href="/docs/features/pages" class="inline-block relative px-4 py-2 w-full text-xs font-medium text-center text-white no-underline bg-transparent rounded-full ring-1 opacity-70 group-hover:opacity-100 group ring-white/20 md:w-auto">
        <span>Learn more about pages</span>
        <span class="text-[#e66735] group-hover:translate-x-1 inline-block ml-0.5 ease-out duration-300">&rarr;</span>
    </a>
</div>

### Layouts

Design **layouts** that multiple pages can utilize.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{title}</title>
</head>
<body>
    {slot}
</body>
</html>
```

Then, use it in any page.

```
<layout title="Radical Righteousness" src="main.html">

    <h1>🏄‍♂️ Totally Tubuloso Website</h1>
    
</layout>
```

<div class="flex justify-end my-8">
    <a href="/docs/features/layouts" class="inline-block relative px-4 py-2 w-full text-xs font-medium text-center text-white no-underline bg-transparent rounded-full ring-1 opacity-70 group-hover:opacity-100 group ring-white/20 md:w-auto">
        <span>Learn more about layouts</span>
        <span class="text-[#e66735] group-hover:translate-x-1 inline-block ml-0.5 ease-out duration-300">&rarr;</span>
    </a>
</div>

### Includes

Create re-usable HTML partials with the `<include>` tag. Specify the HTML file with the `src` attribute.

```
<layout title="Behind the Scenes!" src="main.html">

    <include src="about-header.html"></include>
    <include src="about-copy.html"></include>

</layout>
```

<div class="flex justify-end my-8">
    <a href="/docs/features/pages" class="inline-block relative px-4 py-2 w-full text-xs font-medium text-center text-white no-underline bg-transparent rounded-full ring-1 opacity-70 group-hover:opacity-100 group ring-white/20 md:w-auto">
        <span>Learn more about includes</span>
        <span class="text-[#e66735] group-hover:translate-x-1 inline-block ml-0.5 ease-out duration-300">&rarr;</span>
    </a>
</div>

## Start your first site

Getting started with Static is super easy. The first thing that you'll want to do is install the **Static CLI** command globally. Make sure you have the pre-requisites installed, and then inside of your command line you can run:

<div class="p-5 font-mono whitespace-break-spaces bg-white/[6%] rounded-xl border border-white/[8%]"><span class="text-pink-400">npm install</span> <span class="text-green-400">-g</span> <span class="text-yellow-400">@devdojo/static</span>
</div>

Now that you have the **Static CLI** command installed you can create a new static website by running:

<div class="p-5 font-mono whitespace-break-spaces bg-white/[6%] rounded-xl border border-white/[8%]"><span class="text-pink-400">static</span> <span class="text-green-400">new</span> <span class="text-yellow-400">folder-name</span>
</div>

You can run this command from any directory and it will create a new website inside of the `folder-name` that you specified.

Boom 💥 That's it you're now ready to start building your next masterpeice.