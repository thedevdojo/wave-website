---
title: Static Page-based Routing
description: Learn about the page-based routing system in Static and how to use it.
nextTitle: 'Layouts'
nextURL: '/docs/features/layouts'
prevTitle: 'Folder Structure'
prevURL: '/docs/guides/folder-structure' 
---

<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:h-20 md:block" src="/assets/images/icons/page-globe.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Page-based Routing</h1>
      <p class="my-1">Static uses a simple page-based routing system where each route is mapped to a file inside of a <strong>pages</strong> directory. This allows you to easily create routes for your website by adding files to this directory.</p>
   </div>
</div>


<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-blue-600 border-l-4 border-blue-800 rounded-md">
    <img class="w-auto h-8 mr-3.5 my-0" src="/assets/images/icons/info.png" />
    <span>If you used the <code>static new</code> command, a <strong>pages</strong> directory will automatically be created. If you are inside an empty folder, you can just create a new folder with the name of <strong>pages</strong>.</span>
</div>

## Creating Pages

There are two ways to create a route for your website using page-based routing in Static:

1. **Adding an index.html file to a folder:** If you add an index.html file to a folder inside the pages directory, it will serve as the homepage of your application. For example, adding a file located at `/pages/about/index.html` would serve up an `/about` page.

2. **Adding a file directly to the pages directory:** You can also add files directly to the pages directory to create routes. For example, adding a file located at `/pages/about.html` would resolve to the `/about` page.

Creating pages for your website is as simple as adding a new file to your `pages` directory. When you add a new page it will automatically create a corresponding route for that page.

## Route Structure

The structure of the pages directory determines the routes available on your website. Each file within the pages directory corresponds to a route. For example, with a structure like this:

<div class="p-5 font-mono whitespace-break-spaces bg-white/[6%] rounded-xl border border-white/[8%]"><span class="text-green-400">📁 pages</span>
<span class="text-green-400"><span class="text-yellow-400">├──</span> 📄 index.html</span>
<span class="text-green-400"><span class="text-yellow-400">├──</span> 📄 about.html</span>
<span class="text-green-400"><span class="text-yellow-400">├──</span> 📁 contact</span>
<span class="text-green-400"><span class="text-yellow-400">│   ├──</span> 📄 index.html</span>
<span class="text-green-400"><span class="text-yellow-400">│   ├──</span> 📁 form</span>
<span class="text-green-400"><span class="text-yellow-400">│   │   ├──</span> 📄 index.html</span>
</div>

Your website will have the following routes available:

<div class="p-5 font-mono whitespace-break-spaces bg-white/[6%] rounded-xl border text-gray-400 border-white/[8%]">http://localhost:3000<span class="text-green-400">/</span>
http://localhost:3000<span class="text-green-400">/about</span>
http://localhost:3000<span class="text-green-400">/contact</span>
http://localhost:3000<span class="text-green-400">/contact/form</span>
</div>

## Re-using Pages

There may be times when you want to create a page that resolves to multiple routes. You can do this without having to duplicate a page. Use the `<page>` tag to load the contents of another page.

```html
<page src="learn/index.html"></page>
```

Wherever you place this file, it will generate a route for that page and load the same contents as the HTML file referenced in the **src** attribute.

---

That's the basics of Page-based routing. Next, let's move on to layouts.