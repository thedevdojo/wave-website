---
title: Local Development
description: Learn about the steps you need to perform local development on your app
prevTitle: 'Installation'
prevURL: '/docs/install'
nextTitle: 'Authentication'
nextURL: '/docs/auth'
---

# Local Development

Wave leverages all the latest technologies of a Laravel 11 application. This includes running <a href="https://vitejs.dev/" target="_blank">Vite</a> for compiling your local assets. Let's learn more about the commands you need to run to compile your assets and get hot reloading working.

## Install Node Dependencies

From your project folder, run the following command:

```shell
npm install
```

This will install all the dependencies that are definied inside of the package.json file which include Tailwind, Alpine, and Vite.

## Start your Asset Watcher

After you've installed the node dependencies, you'll then need to run:

```
npm run dev
```

This will start your assets watcher which checks for changes made to your codebase and hot-reloads the current page you are viewing. It will also check all the tailwind CSS classes that need to be used in your project and inject them into your page.

## Building Assets for Production

When you are ready to build your assets and push your code to production you will want to run:

```
npm run build
```

This will compile all your assets and save them to a minified file, making your application run quicker and better optimized for SEO.

## Themes

Wave has the concept of **Themes** which means you can change the way your application looks by changing your theme. When you start your asset watcher or build your assets it will watch and build the assets for the current active theme. We'll cover this in more detail in the themes section 😉

