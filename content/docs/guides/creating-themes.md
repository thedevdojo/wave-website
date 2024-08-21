---
title: Creating Themes
description: Learn how you can host your website and make it live for the world to see.
nextTitle: ''
nextURL: null
prevTitle: 'About Guides'
prevURL: '/docs/guides/about' 
---

# Creating Themes

It will probably be beneficial to learn how to create a simple theme for Wave, so that's what we'll cover in this quick guide.

- [Creating Themes](#creating-themes)
    - [The Simplest Theme](#the-simplest-theme)
    - [Add a homepage view](#add-a-homepage-view)
    - [Creating Your Assets](#creating-your-assets)
    - [Example Theme](#example-theme)


### The Simplest Theme

Creating your own theme is as easy as creating a new folder inside of `resources/themes`. The name of this folder should be the name of your theme in all lowercase letters (Example: `resources/views/example`). Next, we need to add a `theme.json` inside of the theme folder with the following contents:

```json
{
	"name": "Example",
	"version": "1.0"
}
```

In this *.json* file you will specify the `name` of the theme and the `version`. 

That's it! You should now see this theme inside of the admin; however, you will see a broken image because you haven't added an image yet. That is why the recommended minimum for any theme is:

1. theme.json - (containing information about the theme)
2. theme.jpg - (containing a screenshot/cover of the theme)

That's really all that's needed to create a theme; however, you will get an error when you try and visit the homepage and other areas of the application because you haven't created those views yet.

### Add a homepage view

Because each theme utilizes **Folio/Volt pages**, we can simply create a new **pages** folder with an **index.blade.php** file. (Example: `resources/themes/example/pages/index.blade.php).

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Example Theme</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="flex justify-center items-center w-screen h-screen">
    <div class="relative text-center">
        <h1 class="mb-3 text-4xl font-light">Example Theme</h1>
        <p>This is a simple example of a blank theme. <a href="https://devdojo.com/wave/docs" target="_blank" class="underline">Click here to view the docs</a></p>
    </div>
</body>
</html>
```

Add that HTML to your **index.blade.php** file and you will now be able to visit the homepage of your application and see this view.

You can do the same for the dashboard by creating a file at `resources/themes/example/pages/dashboard/index.blade.php` and you will now be able to visit your application `/dashboard` route.

As you can see you can do this with any other pages in your application, it might be good to look at one of the current themes to see all the pages that are created.

### Creating Your Assets

You probably do not want to load the Tailwind CSS Cdn link, like we've showed in the example HTML file. Instead, you'll probably want to create your own `app.css` and `app.js` this way you can use the **vite** asset builder to compile your assets. Create the two following files:

1. resources/themes/example/assets/css/app.css
2. resources/themes/example/assets/js/app.js

> You will want to swap out `example` with the name of your folder.

Next, add the following contents to your `app.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

You can also add any javascript that you want to your `app.js`. Remember you do not need to include Alpine or Livewire javascript from this file because they will automatically be injected since we are using the latest version of Livewire.

Next, we want to reference our `app.css` and our `app.js` from our application, so inside the head of your layout or the `pages/index.blade.php`, we can add the following:

```
@vite(['resources/themes/anchor/assets/css/app.css', 'resources/themes/anchor/assets/js/app.js'])
```

You will also want to add the **filament** and the **livewire** styles. Be sure to include those before the **@vite** helper:

```
@filamentStyles
@livewireStyles
@vite(['resources/themes/example/assets/css/app.css', 'resources/themes/example/assets/js/app.js'])
```

> Important: Make sure to add the filament and livewire styles before your vite helper. Adding them after may result in some mis-aligned styles.

The final result should look something like this:

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
<body class="flex justify-center items-center w-screen h-screen">
    <div class="relative text-center">
        <h1 class="mb-3 text-4xl font-light">Example Theme</h1>
        <p>This is a simple example of a blank theme. <a href="https://devdojo.com/wave/docs" target="_blank" class="underline">Click here to view the docs</a></p>
    </div>
</body>
</html>
```

Now, you'll be able to run `npm run dev` and your theme will be hot-reloading 🔥

When you're ready to compile your assets for production you can run `npm run build` and the correct theme assets will be minified and saved to your public directory.

### Example Theme

If you want to reference this example theme that we've created in this example to use it as a starting point for your theme, you can find the <a href="https://github.com/thedevdojo/example" target="_blank">Example Theme here</a>.