---
title: Static Content
description: Learn how to add content to your website
nextTitle: 'Live-Reloading'
nextURL: '/docs/features/live-reloading'
prevTitle: 'Collections'
prevURL: '/docs/features/collections'
---

<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="w-auto h-12 my-0 mr-5 md:h-20 md:block hidden" src="/assets/images/icons/content.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Content</h1>
      <p class="my-1">Learn how to create and manage content for your Static website using Markdown files and content pages.</p>
   </div>
</div>

## About Content

The content for your website will live inside a `content` folder, located in the root of your project. 

<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-blue-600 border-l-4 border-blue-800 rounded-md">
    <img class="w-auto h-8 mr-3.5 my-0" src="/assets/images/icons/info.png" />
    <span>Don't see this folder? You can simply create a new folder and name it <code>content</code>.</span>
</div>

> Content is written in <a href="https://www.markdowntutorial.com/" class="text-yellow-400 underline">Markdown</a>, a simple syntax that can be used to add headings, lists, links, and other formatting elements represented with only text. <a href="https://www.markdowntutorial.com/" class="text-yellow-400 underline">Learn more about Markdown here</a>.

## Creating Content

To create a new piece of content you add a new file with a `.md` extension to the `content` folder.

Any file in this directory will be mapped to a route, similar to page-based routing. Here's an example:

<div class="py-3.5 px-5 font-mono text-xs text-neutral-400 font-bold border rounded-md bg-neutral-950 border-neutral-800">📄 content/docs/index.md</div>

```makefile
---
title: Welcome to the Docs
description: Add a description here
---

Welcome to the docs. This is an example markdown file.

## About

Learn more about...
```

If this file above were located at `content/docs/index.md`, it would create a new route at `https://localhost:3000/docs`.

## Content Pages

Content pages will attempt to use the HTML from the **pages** directory that has the same path. For instance, if we had a content file located at `content/docs/index.md`, static will use the HTML from a located at `pages/docs/index.html`.

<div class="py-3.5 px-5 font-mono text-xs text-neutral-400 font-bold border rounded-md bg-neutral-950 border-neutral-800">📄 pages/docs/index.html</div>

```html
<layout src="main.html" title="{frontmatter.title}">
   
    <article class="prose prose-md">
        {content}
    </article>
    
</layout>
```

A content page works exactly like any other page; however, it is expected to have a `{content}` shortcode, which is where the **content** will be rendered.

The same HTML can be used for multiple pieces of content. If we had a page at `pages/docs/index.html`, it would be used for all content inside of `content/docs/*.md`. Or, you can choose to create a separate page for individual pieces of content. As an example, a page located at `pages/blog/coding.html` would be used for a content file located at `content/blog/coding.md`. Static will look for a corresponding file, and if it does not exist, it will traverse down the directory until it finds a page, like so:

<div class="px-4 mt-6 text-base font-medium border rounded-md border-neutral-700 bg-neutral-900">
<p class="flex items-center space-x-2"><span class="text-green-400">FIND</span> <span class="text-yellow-400">pages/blog/coding.html</span> <span class="text-pink-400">(use page if exists, if not 👇)</span></p>
<p><span class="text-green-400">FIND</span> <span class="text-yellow-400">pages/blog/index.html</span> <span class="text-pink-400">(use page if exists, if not 👇)</span></p>
<p><span class="text-green-400">FIND</span> <span class="text-yellow-400">pages/blog.html</span> <span class="text-pink-400">(use page if exists, if not 👇)</span></p>
<p><span class="text-green-400">FIND</span> <span class="text-yellow-400">pages/index.html</span> <span class="text-pink-400">(use page or throw error)</span></p>
</div>

<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-purple-600 border-l-4 border-purple-800 rounded-md">
    <img class="w-auto h-12 mr-3.5 my-0" src="/assets/images/icons/book-question.png" />
    <span class="leading-tight opacity-80">If you have a page template located at <strong>/pages/blog/index.html</strong> and you want to use a separate template for the content page, you can add a file called <strong>[content].html</strong> inside that folder, and it will be used instead of the <strong>index.html</strong></span>
</div>

## Content Frontmatter

At the beginning of every Markdown file you will add **frontmatter** to the top of the file, which displays information about that specific content. Here's an example:

```makefile
---
title: My Awesome Content
date: 2022-01-01
active: true
---
```

Frontmatter is written in YAML and is enclosed between --- delimiters. Frontmatter allows users to define variables and values that can be accessed and used within the page.

### Using Frontmatter in HTML


In the example above, the frontmatter defines three variables: title, date, and active. These variables can be accessed and used within a pages HTML code by enclosing them in curly braces `{}`. For example, to display the title from the frontmatter, they can use `{frontmatter.title}`.

Here's an example of using frontmatter variables in HTML:

```html
<h1>{frontmatter.title}</h1>
<p>Date: {frontmatter.date}</p>
```

### Using Conditionals with Frontmatter

Users can also use conditionals to control the display of content based on frontmatter values. They can use the `<If>` tag with a condition attribute to conditionally render HTML elements.

Here's an example of using conditionals with frontmatter:

```
<If condition="frontmatter.active == true">
    <p>This content is active.</p>
</If>
```

In the example above, the <p> element will only be displayed if the `active` variable in the frontmatter is `true`.
 
### Accessing Frontmatter with JavaScript

A global JavaScript variable called `frontmatter` is also made available to access the values using javascript. You can use this variable to extract and use frontmatter data dynamically.

Here's an example of accessing frontmatter with JavaScript:

```javascript
console.log(frontmatter.title); // Output: My Awesome Content
console.log(frontmatter.date); // Output: 2022-01-01
console.log(frontmatter.active); // Output: true
```
## Content Loops

Content loops use the `<ForEach></ForEach>` tags to loop through content. They function the same way as collection loops; however, you will use the `content` attribute as opposed to the `collection` attribute.

```html
<ForEach content="posts">
    <h2><a href="{posts.link}">{posts.title}</a></h2>
    <p>{posts.excerpt}</p>
</ForEach>
```

You can also make use of the **as**, **orderBy**, and **count** attributes.

```html
<ForEach content="posts" as="post" orderBy="date" count="3">
    <h2>{post.title}</h2>
</ForEach>
```

This loop will fetch three posts, ordered by the **date** and referenced as **post**, from the **content/posts** folder.

<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-pink-500 border-l-4 border-pink-700 rounded-md">
    <img class="w-auto h-12 mr-3.5 my-0" src="/assets/images/icons/cards.png" />
    <span class="block">
        <span class="block mb-1 text-sm font-black">Fun Fact:</span>
        <span class="leading-tight opacity-80">Under the hood <strong>content loops</strong> will generate <strong>collections</strong> at run time. This is why <strong>collection loops</strong> and <strong>content loops</strong> function the same.
    </span>
</div>


You may also utilize `<If></If>` tags to conditionally render data in your content. The **conditionals** functionality will be the same as it is in collections.