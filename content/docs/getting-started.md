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

## Getting Started

**Static** is a static site generator you're going to love. Here's the spiel:

- Static is **easy**. 
- HTML is **easy**. 
- Yet, somehow we lost the art of **crafting simple** HTML websites

Static is going to help you rediscover your joy and excitement for building HTML websites.

## Why Static

Most <strong>Static Site Generators</strong> (SSG's) **are overkill** and packed with unnecessary complexities. These complexities have frequently led to frustration, anger, and a strong desire to set fire to the office 🔥

<div class="flex items-center px-4 py-4 my-6 leading-[24px] bg-blue-600 border-l-4 border-blue-800 rounded-md">
<img class="w-auto h-8 mr-3.5 my-0" src="/assets/images/icons/info.png" />
<span>This is where Static comes into play. Static is here to make things simple, bring you joy, and help you regain control over any desire to start fires.</span>
</div>


Generating static websites can be simple and enjoyable again without the need for bloated frameworks and complicated configs. Check out a few of the key features below.

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

<div class="flex justify-end my-8 ">
    <a href="/docs/features/pages" class="relative inline-block w-full px-4 py-2 text-xs font-medium text-center text-white no-underline bg-transparent rounded-full opacity-70 group-hover:opacity-100 group ring-1 ring-white/20 md:w-auto">
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

<div class="flex justify-end my-8 ">
    <a href="/docs/features/layouts" class="relative inline-block w-full px-4 py-2 text-xs font-medium text-center text-white no-underline bg-transparent rounded-full opacity-70 group-hover:opacity-100 group ring-1 ring-white/20 md:w-auto">
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

<div class="flex justify-end my-8 ">
    <a href="/docs/features/pages" class="relative inline-block w-full px-4 py-2 text-xs font-medium text-center text-white no-underline bg-transparent rounded-full opacity-70 group-hover:opacity-100 group ring-1 ring-white/20 md:w-auto">
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