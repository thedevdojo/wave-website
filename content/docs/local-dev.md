---
title: Local Development
description: Learn about the steps you need to perform local development on your app
prevTitle: 'Installation'
prevURL: '/docs/install'
nextTitle: 'Upgrading'
nextURL: '/docs/upgrading'
---

# Local Development

Wave utilizes the <a href="https://laravel.com/docs/vite" target="_blank">Laravel Vite plugin</a> for compiling assets and enabling hot-reloading. Let's set it up below.

## Install Node Dependencies

From your project folder, run the following command:

<div class="p-5 font-mono whitespace-break-spaces bg-neutral-800 text-sm rounded-xl border border-white/[8%]"><span class="text-[#62d6e8]">npm</span> <span class="text-[#f8e164]">install</span></div>

This will install many dependencies including <a href="https://tailwindcss.com" target="_blank">Tailwind</a>, <a href="https://alpinejs.dev" target="_blank">Alpine</a>, and <a href="https://vite.dev" target="_blank">Vite</a>.

## Start your Asset Watcher

After you've installed the node dependencies, you'll then need to run:

<div class="p-5 font-mono text-sm bg-neutral-800 rounded-xl whitespace-break-spaces"><span class="text-[#62d6e8]">npm</span> <span class="text-[#f8e164]">run</span> <span class="text-[#f8e164]">dev</span></div>

This will start your asset watcher, which listens for any changes made to your codebase. When a change is detected, it refreshes the current page and dynamically injects the necessary Tailwind CSS classes.

## Building Assets for Production

When you are ready to build your assets and push your code to production you will want to run:

<div class="p-5 font-mono text-sm bg-neutral-800 rounded-xl whitespace-break-spaces"><span class="text-[#62d6e8]">npm</span> <span class="text-[#f8e164]">run</span> <span class="text-[#f8e164]">build</span></div>

This will compile and minify all your assets, resulting in a faster application and an improved experience.

## Themes

Wave supports **Themes**, allowing you to change the appearance of your application simply by switching themes. When you start your asset watcher or build your assets, it will automatically handle the assets for the currently active theme. We'll explore this further in the themes section.

