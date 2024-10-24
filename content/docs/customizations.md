---
title: Customizations
description: Learn how to add some basic customizations to your application
prevTitle: 'Local Development'
prevURL: '/docs/local-dev'
nextTitle: 'Your Functionality'
nextURL: '/docs/your-functionality'
---

# Customizations

You can customize your application as much as you would like; however, there are a handful of things that you'll immediately want to customize such as logos, favicons, and colors.

- [Customizations](#customizations)
  - [Change Your Logo](#change-your-logo)
  - [Change Your Favicon](#change-your-favicon)
  - [Change the Default Color](#change-the-default-color)
  - [Authentication Views](#authentication-views)

---

## Change Your Logo

There are two files that you will want to change to add your own custom logo. Those files are:

 - resources/views/components/logo.blade.php
 - resources/views/components/logo-icon.blade.php

In each of these files, you will see an SVG, similar to the following:

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="resources/views/components/logo.blade.php"></include>
```
<svg {{ $attributes->merge(['class' => 'text-gray-900 dark:text-white']) }} xmlns="..."></svg>
```
</div>

 - **logo.blade.php** - In this file you will want to add your full logo. This typically includes your logo icon with the name of your SaaS next to the logo.

 - **logo-icon.blade.php** - In this file you will want to add your logo icon. This can be used in various places where you don't want to show the full logo, but only the logo icon.

In each of these files, you will want to replace the contents with your own **svg** logo, or you can include an **img** tag with your logo src.

**Be sure to include the `$attributes` tag in your image or your SVG**

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html"></include>
```
{{ $attributes->merge(['class' => 'text-gray-900 dark:text-white']) }}
```
</div>

This will gaurantee that when the logo is used in your view files that it will forward any classes, like so:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html"></include>
```
<x-logo class="h-8" />
```
</div>

In this case it will also pass the `h-8` class to the component.

## Change Your Favicon

To change the favicon for your application you will want to replace the following images:

- public/wave/favicon.png - default favicon
- public/wave/favicon-dark.png - favicon to show in dark mode

You will also want to add a `favicon.ico` to the `/public` directory to support older browsers.

> Try to make sure that your favicon pngs are at least 180x180px. If you want to customize how these favicons are loaded you can modify the component located at `resources/views/components/favicon.blade.php`

## Change the Default Color

Inside of your `config/wave.php` you'll see a value called **primary_color**, like so:

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="config/wave.php"></include>
```php
'primary_color' => '#000000',
```
</div>

Change this to any HEX color value and that will be the primary color used for buttons, input focus, and more.

## Authentication Views

We are utilizing DevDojo Auth, which means you can customize all the authentication views by visiting the **setup** page at `/auth/setup`. Here you can change the alignment, color, logo, and more.

<img src="https://devdojo.com/auth/assets/images/setup-screen-bg.jpg" class="w-full rounded-md" />

Learn more about customizing your authentication views in the official <a href="https://devdojo.com/auth/docs/setup-customizations/" target="_blank">DevDojo Auth documentation here</a>.