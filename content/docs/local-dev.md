---
title: Local Development
description: Learn about the steps you need to perform local development on your app
prevTitle: 'Installation'
prevURL: '/docs/install'
nextTitle: 'Upgrading'
nextURL: '/docs/upgrading'
---

# Local Development

Wave leverages all the latest technologies of a Laravel 11 application. This includes running <a href="https://vitejs.dev/" target="_blank">Vite</a> for compiling your local assets. Let's learn more about the commands you need to run to compile your assets and get hot reloading working.

## Install Node Dependencies

From your project folder, run the following command:

<div class="p-5 font-mono whitespace-break-spaces bg-gray-800 text-sm rounded-xl border border-white/[8%]"><span class="text-[#62d6e8]">npm</span> <span class="text-[#f8e164]">install</span></div>

This will install all the dependencies that are definied inside of the package.json file which include Tailwind, Alpine, and Vite.

## Start your Asset Watcher

After you've installed the node dependencies, you'll then need to run:

<div class="p-5 font-mono text-sm bg-gray-800 rounded-xl whitespace-break-spaces"><span class="text-[#62d6e8]">npm</span> <span class="text-[#f8e164]">run</span> <span class="text-[#f8e164]">dev</span></div>

This will start your assets watcher which checks for changes made to your codebase and hot-reloads the current page you are viewing. It will also check all the tailwind CSS classes that need to be used in your project and inject them into your page.

## Building Assets for Production

When you are ready to build your assets and push your code to production you will want to run:

<div class="p-5 font-mono text-sm bg-gray-800 rounded-xl whitespace-break-spaces"><span class="text-[#62d6e8]">npm</span> <span class="text-[#f8e164]">run</span> <span class="text-[#f8e164]">build</span></div>

This will compile all your assets and save them to a minified file, making your application run quicker and better optimized for SEO.

## Themes

Wave has the concept of **Themes** which means you can change the way your application looks by changing your theme. When you start your asset watcher or build your assets it will watch and build the assets for the current active theme. We'll cover this in more detail in the themes section 😉

