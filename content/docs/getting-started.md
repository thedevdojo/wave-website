---
title: Getting Started with Wave
description: This is the introduction and getting started seciton for the Wave Docs
slug: 'getting-started'
prevTitle: null
prevURL: null
nextTitle: 'Installation'
nextURL: '/docs/install'
home: true
---

# Introduction

Welcome to Wave, the **SaaS Starter Kit** that will help you ship your next idea fast. This documentation will be your guide to navigating the Seas of SaaS development.

<div class="flex relative items-center py-5 pr-5 pl-[140px] my-10 leading-normal text-white bg-linear-to-br from-blue-500 to-indigo-600  rounded-md">
<img src="https://cdn.devdojo.com/images/march2021/octocat-help.png" class="absolute left-0 shrink-0 my-0 mt-2 mr-3.5 ml-2 w-auto h-32" /> 
<svg  class="hidden shrink-0 my-0 mr-3.5 w-auto h-10" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 60 60" fill="none"><path fill="#000" d="M31.644 46.367c0 1.733-1.39 3.14-3.099 3.14-1.713 0-3.104-1.406-3.104-3.14 0-1.734 1.39-3.142 3.104-3.142 1.71.003 3.1 1.408 3.1 3.142ZM22.612 23.744c1.374-5.633 14.076-3.948 12.957 2.825-.42 2.529-4.902 2.312-6.74 3.229-2.906 1.446-3.56 4.312-2.744 7.304.958 3.52 6.357 2.023 5.395-1.504-.392-1.435 1.367-1.188 2.83-1.52 1.907-.428 3.508-1.184 4.877-2.604 3.586-3.714 1.903-9.437-.885-12.964-4.994-6.328-19.082-4.49-21.08 3.726-.866 3.548 4.529 5.052 5.39 1.508Z"/><path fill="#000" d="M58.14 16.805C51.474-1.52 30.006-1.86 14.194 1.906c-3.467.825-2.053 6.147 1.362 5.477-11.78 7.305-19.67 20.77-13.275 34.938 7.496 16.613 30.228 23.27 44.856 12.3C58.267 46.278 62.9 29.886 58.14 16.805ZM47.876 46.142c-8.345 10.456-21.959 9.987-32.526 3.36-10.22-6.404-11.375-18.73-5.916-28.64 5.378-9.758 16.414-14.18 26.986-13.395 1.015.077 1.73-.329 2.175-.942 5.54 1.446 10.4 4.585 13.521 10.41 4.897 9.137 1.91 21.503-4.24 29.207Z"/></svg>
<span>Be sure to <a href="https://github.com/thedevdojo/wave" target="_blank" class="text-white underline">give us a star on Github</a>. The more stars we get 🤩 the more time we can spend on making Wave even better.</span>
</div>

- [Introduction](#introduction)
  - [About Wave](#about-wave)
    - [Key Features](#key-features)
    - [Under The Hood](#under-the-hood)
  - [Demo](#demo)
  - [Installation](#installation)

## About Wave

**Wave** is built on top of the popular <a href="https://laravel.com" target="_blank">Laravel Framework</a>. It's not necessary that you know Laravel; however, a basic understanding of the framework will definitely help.

Wave has been built with the intention of helping anyone build their next great idea at no cost. Wave provides features found in many popular SaaS platforms, which will save you hundreds of hours.

### Key Features

Below is a list of Waves key features. Click a feature to learn more.

 - <a href="{ url('/docs/features/auth') }">**Authentication**</a>
 - <a href="{ url('/docs/features/user-profiles') }">**User Profiles**</a>
 - <a href="{ url('/docs/features/user-impersonations') }">**User Impersonations**</a>
 - <a href="{ url('/docs/features/billing') }">**Billing**</a>
 - <a href="{ url('/docs/features/subscription-plans') }">**Subscription Plans**</a>
 - <a href="{ url('/docs/features/roles-permissions') }">**Roles and Permissions**</a>
 - <a href="{ url('/docs/features/notifications') }">**User Notifications**</a>
 - <a href="{ url('/docs/features/changelog') }">**Changelog**</a>
 - <a href="{ url('/docs/features/blog') }">**Blog**</a>
 - <a href="{ url('/docs/features/pages') }">**Pages**</a>
 - <a href="{ url('/docs/features/api') }">**API**</a>
 - <a href="{ url('/docs/features/admin') }">**Admin**</a>
 - <a href="{ url('/docs/features/themes') }">**Themes**</a>
 - <a href="{ url('/docs/features/plugins') }">**Plug-ins**</a>

### Under The Hood

Below is a list of technologies that are being used to power the propellers and steer the ship.

**Technologies Used**

- <a href="https://laravel.com" target="_blank" class="font-bold">Laravel</a>
- <a href="https://livewire.laravel.com" target="_blank" class="font-bold">Livewire</a>
- <a href="https://tailwindcss.com" target="_blank" class="font-bold">Tailwind CSS</a>
- <a href="https://alpinejs.dev" target="_blank" class="font-bold">Alpine</a>
- <a href="https://vitejs.dev/" target="_blank" class="font-bold">Vite</a>

Along with many technologies, Wave also utilizes a handful of packages.

**Packages Used**

- <a href="https://filamentphp.com" target="_blank" class="font-bold">FilamentPHP</a>
- <a href="https://devdojo.com/auth" target="_blank" class="font-bold">DevDojo Auth</a>
- <a href="https://github.com/thedevdojo/themes" target="_blank" class="font-bold">DevDojo Themes</a>
- <a href="https://github.com/404labfr/laravel-impersonate" target="_blank" class="font-bold">Impersonation Package</a>
- <a href="https://spatie.be/docs/laravel-permission" target="_blank" class="font-bold">Spatie Roles (Permissions) Package</a>
- <a href="https://laravel.com/docs/folio" target="_blank" class="font-bold">Laravel Folio</a>
- <a href="https://livewire.laravel.com/docs/volt" target="_blank" class="font-bold">Laravel Volt</a>

## Demo

<a href="{ url('/demo') }" target="_blank">View the demo here</a>. The demo utilizes the sandbox billing features, allowing you to test the process. For a complete experience, <a href="{ url('/docs/install') }">install a local copy</a>.

## Installation

Next, let's dive into installing a local copy of Wave.
