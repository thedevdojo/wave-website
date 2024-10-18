---
title: Creating Themes
description: Learn how you can host your website and make it live for the world to see.
prevTitle: 'Global Helpers'
prevURL: '/docs/concepts/global-helpers'
nextTitle: 'Volt Pages'
nextURL: '/docs/concepts/volt'
---

# Creating Themes

In this guide, we'll cover the basics of creating a simple theme for Wave.

- [Creating Themes](#creating-themes)
    - [The Simplest Theme](#the-simplest-theme)
    - [Add a homepage view](#add-a-homepage-view)
    - [Creating Your Assets](#creating-your-assets)
    - [Example Theme](#example-theme)


### The Simplest Theme

Creating a theme is as simple as creating a new folder inside `resources/themes`. The folder name should be in lowercase (e.g., `resources/views/example`). Next, add a `theme.json` file inside the folder with the following contents:

```json
{
	"name": "Example",
	"version": "1.0"
}
```

In this *theme.json* file, specify the `name` of the theme and the `version`. 

That’s it! You should now see this theme in the admin panel; however, you will see a broken image because you haven’t added a screenshot yet. That is why the recommended minimum for any theme is:

1. theme.json - (containing information about the theme)
2. theme.jpg - (containing a screenshot/cover of the theme)

While this is enough to create a theme, visiting the homepage or other sections will trigger errors because the necessary views haven’t been created yet.

### Add a homepage view

Since each theme uses **Folio/Volt pages**, you can create a **pages** folder and add an **index.blade.php** file. (ex: `resources/themes/example/pages/index.blade.php).

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Example Theme</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="flex items-center justify-center w-screen h-screen">
    <div class="relative text-center">
        <h1 class="mb-3 text-4xl font-light">Example Theme</h1>
        <p>This is a simple example of a blank theme. <a href="https://devdojo.com/wave/docs" target="_blank" class="underline">Click here to view the docs</a></p>
    </div>
</body>
</html>
```

Once added, you’ll be able to visit your homepage and see this view.

Similarly, for the dashboard, create a file at resources/themes/example/pages/dashboard/index.blade.php, allowing access to the /dashboard route.

You can follow this process for any other pages in your application. It’s a good idea to check an existing theme to see all the pages it includes.

### Creating Your Assets

Instead of loading the Tailwind CSS CDN as shown in the example, you'll likely want to create your own `app.css` and `app.js` files to manage assets using vite. To do this, create the following files:

1. resources/themes/example/assets/css/app.css
2. resources/themes/example/assets/js/app.js

> Replace example with your folder’s actual name.

Next, add the following to `app.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Feel free to add any JavaScript to your `app.js`. You don’t need to include Alpine.js or Livewire’s JavaScript here—they will be automatically injected as we use the latest version of Livewire.

Next, reference your `app.css` and `app.js` files in the <head> section of your layout:

```
@vite(['resources/themes/anchor/assets/css/app.css', 'resources/themes/anchor/assets/js/app.js'])
```

You should also include **filament** and **livewire** styles before the **@vite** helper:

```
@filamentStyles
@livewireStyles
@vite(['resources/themes/example/assets/css/app.css', 'resources/themes/example/assets/js/app.js'])
```

> Important: Ensure you add Filament and Livewire styles before the Vite helper. Adding them afterward may result in misaligned styles.

The final structure should look like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Example Theme</title>
    @filamentStyles
    @livewireStyles
    @vite(['resources/themes/example/assets/css/app.css', 'resources/themes/example/assets/js/app.js'])
</head>
<body class="flex items-center justify-center w-screen h-screen">
    <div class="relative text-center">
        <h1 class="mb-3 text-4xl font-light">Example Theme</h1>
        <p>This is a simple example of a blank theme. <a href="https://devdojo.com/wave/docs" target="_blank" class="underline">Click here to view the docs</a></p>
    </div>
</body>
</html>
```

Run `npm run dev` to enable hot reloading. 🔥

When you’re ready for production, run `npm run build` to compile and minify your assets for the public directory.

### Example Theme

We've also created an <a href="https://github.com/thedevdojo/example" target="_blank">Example Theme</a> that you may want to use as a starting point when creating your own theme. This theme includes all the essential pages, layouts, and partials you need to create and implement your own custom theme for your SaaS.

You can find the example theme at <a href="https://github.com/thedevdojo/example" target="_blank">https://github.com/thedevdojo/example</a>

If you want to learn more about themes we also have a guide on the <a href="{ url('/docs/guides/theme-structure') }">Structure of a Wave Theme</a>, that will teach you how each theme is structured.

This theme includes all the necessary pages, layouts, and  for all the routes in Wave, so you won’t encounter any missing view errors while navigating through the application. You can download the Example theme from this GitHub repository and customize it to fit your needs.

If you want to reference this example theme that we've created in this example to use it as a starting point for your theme, you can find the <a href="https://github.com/thedevdojo/example" target="_blank">Example Theme here</a>.