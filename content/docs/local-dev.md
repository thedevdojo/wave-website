---
title: Local Development
description: Learn about the steps you need to perform local development on your app
prevTitle: 'Installation'
prevURL: '/docs/install'
nextTitle: 'Customizations'
nextURL: '/docs/customizations'
---

# Local Development

Wave utilizes the <a href="https://laravel.com/docs/vite" target="_blank">Laravel Vite plugin</a> for compiling assets and enabling hot-reloading. Let's set it up below.

## Install Node Dependencies

From your project folder, run the following command:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>
```bash
npm install
```
</div>

This will install many dependencies including <a href="https://tailwindcss.com" target="_blank">Tailwind</a>, <a href="https://alpinejs.dev" target="_blank">Alpine</a>, and <a href="https://vite.dev" target="_blank">Vite</a>.

## Start your Asset Watcher

After you've installed the node dependencies, you'll then need to run:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>
```bash
npm run dev
```
</div>

This will start your asset watcher, which listens for any changes made to your codebase. When a change is detected, it refreshes the current page and dynamically injects the necessary Tailwind CSS classes.

## Building Assets for Production

When you are ready to build your assets and push your code to production you will want to run:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>
```bash
npm run build
```
</div>

This will compile and minify all your assets, resulting in a faster application and an improved experience.

## Themes

Wave supports **Themes**, allowing you to change the appearance of your application simply by switching themes. When you start your asset watcher or build your assets, it will automatically handle the assets for the currently active theme. We'll explore this further in the themes section.

