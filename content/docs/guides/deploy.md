---
title: Deploying Your Website
description: Learn how you can host your website and make it live for the world to see.
nextTitle: 'Folder Structure'
nextURL: '/docs/guides/folder-structure'
prevTitle: 'Github Action'
prevURL: '/docs/features/github-action' 
---


<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:h-20 md:block" src="/assets/images/icons/globe.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Deploying your website</h1>
      <p class="my-1">There are many ways that you can host your website and make your masterpiece live for the world to see.</p>
   </div>
</div>

If you do not want to host your website on Github pages, you can host with a handful of other alternatives.

## Website Build

When you run the `static build` command your website will be built into a new folder named `_site`. This folder will contain all the contents for your website. You can simply move the contents to any server and your site will be served up accordingly.

Remember that if you are hosting your website inside of a subfolder, you will need to pass the full URL to the build command in order for all the assets and images to link up correctly. Here's an example:

```
static build https://my-website/subfolder/
```

## Alternatives

There are a handful of alternatives that you can use to host your site for free. Here are a link to a few of those alternatives below:

- [DigitalOcean](https://m.do.co/c/dc19b9819d06)
- [Cloudflare Pages](https://pages.cloudflare.com/)
- [Firebase](https://firebase.google.com/products/hosting)
- [Static.app](https://static.app/)
- [Netlify](https://www.netlify.com/)
- [Vercel](https://vercel.com/)

## DevDojo Static Hosting

Eventually we'll be providing a free hosted solution where you will get your own `website.devdojo.io` subdomain and have the ability to use your own custom domain. If you want to see this implemented sooner you can can help us out by <a href="https://github.com/thedevdojo/static" target="_blank" class="text-yellow-300 underline">starring the repo</a>, and telling your friends about static 🤘