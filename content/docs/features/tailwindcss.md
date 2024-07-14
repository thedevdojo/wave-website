---
title: TailwindCSS Integration
description: We've built a rock solid integration with TailwindCSS
nextTitle: 'Configurations'
nextURL: '/docs/features/configurations'
prevTitle: 'Live Reloading'
prevURL: '/docs/features/live-reloading' 
---

<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:h-20 md:block" src="/assets/images/icons/tailwindcss.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">TailwindCSS</h1>
      <p class="my-1">Easily use TailwindCSS in your sites by including a simple short code. Learn more about how everything works below.</p>
   </div>
</div>

Including <a href="https://tailwindcss.com" target="_blank" class="text-yellow-300 underline">Tailwind CSS</a> in your project is easier than ever before. 

> It's not required that you use Tailwind, but why wouldn't you? It's the ultimate design library that makes creating your website a breeze. Embrace its power and unleash your creativity!"

## How To Use

To include Tailwind, simply add the `{tailwindcss}` shortcode to the head of your document:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{title}</title>
    <link rel="icon" type="image/x-icon" href="/assets/images/favicon.png">
    {tailwindcss}
</head>
<body>
    {slot}
    <script src="/assets/js/main.js"></script>
</body>
</html>
```

When you use the `static dev` command, the Tailwind CSS CDN will be injected into the page along with all the available plug-ins. Running `static build` will run the **Tailwind CLI** and add all the necessary classes to your `main.css` file.

<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-purple-600 border-l-4 border-purple-800 rounded-md">
    <img class="w-auto h-12 mr-3.5 my-0" src="/assets/images/icons/book-question.png" />
    <span class="leading-5 opacity-80">This shortcode is already added to the main layout in the starter template, so after running <code>static new folder-name</code>, you're ready to start using Tailwind without a build step!</span>
</div>


## How Does It Work

It might be beneficial to understand how it works, and it's pretty simple to explain.

### When Running `static dev`

When you run the `static dev` command, the Tailwind CSS CDN will be injected into the head of your documentation. This also includes all the TailwindCSS Plug-ins.

This will make it easy to test out new colors and styles. You can open up developer tools, add a class and voila! The class will be available because we are using the TailwindCSS CDN. This will also pull in custom styles from your Tailwind config (more info on this below).

Of course, using the Tailwind CDN in production is not recommended, so that's why we handle it differently when you build your site.

### When Running `static build`

When you run the `static build` command we use the Tailwind CLI to search your site for all Tailwind CSS classes that are used. It will then add a minified version of all these classes to your `assets/css/main.css` file. Now, your website should be smokin 🔥 fast!


## Tailwind Configurations

If you are creating a custom template you'll want to create a `tailwind.config.js` to the root of your project, otherwise, if you use a template this should already exist.

<div class="py-3.5 px-5 font-mono text-xs text-neutral-400 font-bold border rounded-md bg-neutral-950 border-neutral-800">📄 tailwind.config.js</div>

```json
/** @type {import('tailwindcss').Config} */
module.exports = {
    content: ["./**/*.{html,js}"],
    theme: {
        extend: {},
    },
    plugins: [
        require('@tailwindcss/typography'),
    ],
}
```

When building for production you'll need to include any plugins you want to use inside of the `plugins` array.

<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-pink-500 border-l-4 border-pink-700 rounded-md">
    <img class="w-auto h-12 mr-3.5 my-0" src="/assets/images/icons/cards.png" />
    <span class="block">
        <span class="block mb-1 text-sm font-black">Does it work in Dev Mode?</span>
        <span class="leading-tight opacity-80">Yes! All the configurations that you add to your config will also be pulled in during dev mode, so you can test custom colors, sizes, and more by adding them to your Tailwind config.
    </span>
</div>
