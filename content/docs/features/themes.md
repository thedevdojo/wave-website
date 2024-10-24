---
title: Themes
description: Learn how to use themes
prevTitle: 'Admin'
prevURL: '/docs/features/admin'
nextTitle: 'Plugins'
nextURL: '/docs/features/plugins'
---

# Themes

You can choose a theme to use as the starting point for your new SaaS. In this section you will learn all about themes and how they work.



- [Themes](#themes)
  - [Chossing a Theme](#chossing-a-theme)
    - [Download Themes](#download-themes)
    - [Installing Themes](#installing-themes)
    - [Activate Themes](#activate-themes)
  - [Theme Views](#theme-views)
  - [Theme Pages](#theme-pages)
  - [Theme Assets](#theme-assets)
    - [Compiling Assets and HMR](#compiling-assets-and-hmr)
    - [Building Assets](#building-assets)
    - [How Does It Work](#how-does-it-work)
  - [Creating Themes](#creating-themes)
    - [The Simplest Theme](#the-simplest-theme)
    - [Add a homepage view](#add-a-homepage-view)
    - [Creating Your Assets](#creating-your-assets)
    - [Example Theme](#example-theme)
  - [Theme Structure](#theme-structure)
    - [Readme.md](#readmemd)
    - [theme.jpg](#themejpg)
    - [theme.json](#themejson)
    - [📁 assets](#-assets)
    - [📁 components](#-components)
    - [📁 pages](#-pages)
    - [📁 partials](#-partials)
  - [Digging Deeper](#digging-deeper)

## Chossing a Theme

When you’re ready to start building, you will want to choose a theme as a starting point for your new SaaS.

### Download Themes

Visit the <a href="{ url('/themes') }" target="_blank">Themes Page</a> to browse available themes for download. Check back often as more themes will be released. Once you’ve downloaded a theme, we’ll need to install it.

### Installing Themes

After <a href="{ url('/themes') }" target="_blank">downloading a theme</a>, extract it move the theme folder to the `resources/themes` directory. For example, if you download the `blank` theme, it should be moved to `resources/themes/blank`.

> You will want to rename the folder to be the name of the theme. As an example if you download the blank theme and it has a folder name of `blank-main`, you'll want to rename it to be `blank`.

### Activate Themes

Now that you have the theme installed, you'll need to head to the admin to activate it. Be sure to login as your admin user and visit <a href="/admin/themes" target="_blank">`/admin/themes`</a> and you’ll see the current themes available in your app.

<img src="https://cdn.devdojo.com/images/august2024/activate-theme.png" class="w-full" alt="Wave Activate Theme" />

To activate a Theme you can simply click the Activate button for the current theme you would like to activate, and that will be the current active theme.

> After activating a theme you may need to make sure that you stop your asset watcher `npm run dev` and re-run it after the new theme has been activated.

## Theme Views

All the views that you need for your application will live inside your `resources/themes/{theme}` folder. When you install Wave, the default theme `anchor` is activated. Therefore all you theme files will be located at `resources/themes/anchor`.

The active theme location is registered in the `theme` view namespace, so as an example if you wanted to reference a `home.blade.php` file inside the active theme you can return a view like so:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
return view('theme::home');
```
</div>

That will return the view located at `resources/themes/anchor/home.blade.php`. 

## Theme Pages

Each theme will have their own `pages` directory that are mapped to a specific route. We'll cover Volt pages in the next section a little more; however, it's probably important to know all the different pages that are provided with each theme.

In addition to all the authentication routes, you will also find the following pages included in each theme.

- **Homepage** - (pages/index.blade.php)
- **Dashboard** - (pages/dashboard/index.blade.php)
- **Pricing** - (pages/pricing/index.blade.php)
- **Profile** - (pages/profile/[username].blade.php)
- **Settings**
    - **Profile Settings** - (pages/settings/profile.blade.php)
    - **Security Settings** - (pages/settings/security.blade.php)
    - **API keys** - (pages/settings/api.blade.php)
    - **Subscription** - (pages/settings/subscription.blade.php)
    - **Invoices** - (pages/settings/invoices.blade.php)
- **Subscription Welcome** - (pages/subscription/welcome.blade.php)
- **Notifications** - (pages/notification/index.blade.php)
- **Blog**
    - **Blog Home/List** - (pages/blog/index.blade.php)
    - **Blog Categories** - (pages/blog/.Wave.Category-slug/index.blad.php)
    - **Blog Post** - (pages/blog/.Wave.Category-slug/[.Wave.Post-slug].blade.php)
- **Changelog**
    - **Changelog Home** - (pages/changelog/index.blade.php)
    - **Changelog Item/Entry** - (pages/changelog/[.Wave.Changelog].blade.php)

## Theme Assets

Every theme will have it's own assets located at the following locations:

1. `resources/themes/{theme}/assets/css/app.css`
2. `resources/themes/{theme}/assets/js/app.js`

When you run your asset watchers and builder using `npm` it will look at these files.

### Compiling Assets and HMR

You can use the common `npm run dev` command to compile your assets and serve them up from your current theme. Running `npm run dev` also supports Hot Module Reloading so when you make a change to any theme file, your assets will automatically be compiled and the browser will refresh.

### Building Assets

When you want to build your assets for production you will run `npm run build`. Wave utilizes the same commands that a default Laravel application supports. You may want to learn more about how to customize and modify your asset builder by visiting the <a href="https://laravel.com/docs/vite" target="_blank">Laravel Vite</a> documentation.

### How Does It Work

Understanding how the asset bundler works can help with debugging or adding functionality. When you  **Activate** a theme, a file named `theme.json` is stored in the root directory with contents resembling the following:

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="theme.json"></include>

```json
{
    "name": "anchor"
}
```
</div>

This file contains the currently active theme, which is referenced inside our `vite.config.js`.

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="vite.config.js"></include>

```js
const themeFilePath = path.resolve(__dirname, 'theme.json');
const activeTheme = fs.existsSync(themeFilePath) ? JSON.parse(fs.readFileSync(themeFilePath, 'utf8')).name : 'anchor';
console.log(`Active theme: ${activeTheme}`);

export default defineConfig({
    plugins: [
        laravel({
            input: [
                `resources/themes/${activeTheme}/assets/css/app.css`,
                `resources/themes/${activeTheme}/assets/js/app.js`,
                'resources/css/filament/admin/theme.css',
            ],
            refresh: [
                `resources/themes/${activeTheme}/**/*`,
            ],
        }),
    ],
});
```
</div>

The `vite` config reads this file to determine the active theme and compiles its assets.

## Creating Themes

To fully control the appearance, you may consider creating your own theme. Even if you don’t plan to create a custom theme, this section will help you understand how themes work. Let’s begin with creating a simple theme.

### The Simplest Theme

Creating a theme is as simple as adding a new folder in the `resources/themes` folder. The folder name should be lowercase (e.g., `resources/views/example`). Then, add a `theme.json` file with the following contents:

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="resources/themes/example/theme.json"></include>

```json
{
    "name": "Example",
    "version": "1.0"
}
```
</div>

This `theme.json` file defines the theme’s **name** and **version**. Next, add an image named `theme.jpg` to your theme folder (e.g., `resources/themes/example/theme.jpg`) with a 16:9 ratio (at least 1280x720px).

<div class="flex items-center px-4 py-4 my-6 text-blue-800 text-xs font-semibold bg-blue-100 border-l-4 border-blue-200 rounded-md">
<span>That’s it! You’ve just created your first theme, and it will now appear in the admin panel ready for activation.</span>
</div>

<div class="flex items-center px-4 py-4 my-6 text-orange-800 text-xs font-semibold bg-orange-100 border-l-4 border-orange-200 rounded-md">
<span>Unfortunately, navigating to any page will result in an error because your theme doesn't haven't any views just yet.</span>
</div>



### Add a homepage view

Since each theme uses Folio and Volt, you can create a `pages` folder and add an `index.blade.php` file.

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="resources/themes/example/pages/index.blade.php"></include>

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
</div>

Once added, you’ll be able to visit your homepage and see this view.

Similarly, for the dashboard, create a file at resources/themes/example/pages/dashboard/index.blade.php, allowing access to the /dashboard route.

You can follow this process for any other pages in your application. It’s a good idea to check an existing theme to see all the pages it includes.

### Creating Your Assets

Instead of loading the Tailwind CSS CDN as shown in the example, you'll most-likely want to create your own `app.css` and `app.js` files to manage assets using vite. To do this, create the following files:

1. resources/themes/example/assets/css/app.css
2. resources/themes/example/assets/js/app.js


> Replace example with your folder’s actual name.

Next, add the following to your theme `app.css`

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="resources/themes/example/assets/css/app.css"></include>

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
</div>

Feel free to add any JavaScript to your `app.js`. You don’t need to include Alpine.js or Livewire’s JavaScript here—they will be automatically injected as we use the latest version of Livewire.

Next, reference your `app.css` and `app.js` files in the <head> section of your layout:

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="resources/themes/example/components/layouts/app.blade.php"></include>

```php
@vite(['resources/themes/anchor/assets/css/app.css', 'resources/themes/anchor/assets/js/app.js'])
```
</div>

You should also include **filament** and **livewire** styles before the **@vite** helper:

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="resources/themes/example/components/layouts/app.blade.php"></include>

```php
@filamentStyles
@livewireStyles
@vite(['resources/themes/example/assets/css/app.css', 'resources/themes/example/assets/js/app.js'])
```
</div>

<div class="flex items-center px-4 py-4 my-6 text-red-800 text-xs font-normal bg-red-100 border-l-4 border-red-200 rounded-md">
<span>Make sure the Filament and Livewire styles are added before the Vite helper. Adding them afterward may result in some unexpected results.</span>
</div>

The final structure should look like this:

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="resources/themes/example/components/layouts/app.blade.php"></include>

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
</div>

<div class="flex items-center px-4 py-4 my-6 text-orange-800 text-xs font-normal bg-orange-100 border-l-4 border-orange-200 rounded-md">
<span>The code in the &lt;head&gt; tag should be applied to both layouts <strong class="text-orange-900">app.blade.php</strong> and <strong class="text-orange-900">marketing.blade.php</strong></span>
</div>

Now, run `npm run dev` to enable hot reloading. When you’re ready for production, run `npm run build` to compile and minify your assets to the public directory.

### Example Theme

We've also created an <a href="https://github.com/thedevdojo/example" target="_blank">Example Theme</a> you can use as a starting point for building your own theme. It includes all the essential pages, layouts, and partials needed to build a custom theme. You can find this example theme at <a href="https://github.com/thedevdojo/example" target="_blank">https://github.com/thedevdojo/example</a>.

Finally, it may be helpful to learn the basic **Structure of a Theme**, let's cover that next.

## Theme Structure

Files and folders inside a theme can vary; however, most will have a similar structure, like the following:

 - Readme.md
 - theme.jpg
 - theme.json
 - **assets (folder)**
 - **components (folder)**
 - **pages (folder)**
 - **partials (folder)**

### Readme.md

This file contains details about the theme, including installation instructions, links, and other relevant info.

### theme.jpg

The cover art image that displays in the admin theme section.

### theme.json

This file holds the name and current version of the theme.

### 📁 assets

The **assets** folder houses your CSS and JavaScript files. By default, it includes:

- `css/app.css`
- `js/app.js`

You can add custom CSS or JS to these files, and they will be automatically included in your application.

### 📁 components

The **components** folder contains reusable components for your theme. It includes four subfolders:

- **app**
- **elements**
- **layouts**
- **marketing**

The **app** folder in the components stores application specific components (non-marketing pages). As an example, in the <a href="https://github.com/thedevdojo/example" target="_blank">Example theme</a>, the **components/app** folder contains a **header.blade.php** file used in the app layout.

The **elements** folder contains shared components that can be used throughout your application. Components inside this folder don’t need the `elements` prefix. For instance, if you had a file named `button.blade.php` file inside of the elements folder, you can reference it like this:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```
<x-button>Button Text</x-button>
```
</div>

instead of this:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```
<x-elements.button>Button Text</x-elements.button>
```
</div>

The **marketing** folder holds components used on marketing pages, such as headers, hero sections, features, and more.

The **layouts** folder contains layouts, and every theme comes with two layouts:

 - **app.blade.php** (for authenticated users)
 - **marketing.blade.php** (for guest users)


### 📁 pages

The pages folder is mapped directly to routes via <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a>. For example:

- pages/index.blade.php => **url.com**
- pages/dashboard/index.blade.php => **url.com/dashboard**
- pages/pricing/index.blade.php => **url.com/pricing**
- pages/profile/[username].blade.php => **url.com/profile/johndoe**

... etc.

You can also leverage <a href="https://laravel.com/docs/folio#route-parameters" target="_blank">Route Parameters</a>, <a href="https://laravel.com/docs/folio#route-model-binding" target="_blank">Route Model Binding</a> with Folio.

Additionally, these files support creating single-file <a href="https://livewire.laravel.com/docs/volt" target="_blank">Volt components</a> by adding logic at the top of the view and using the **@volt** directive. Learn <a href="{ url('/docs/features/volt') }">more about that here</a>.

The **pages** folder is where you’ll spend a lot of time adding logic to your SaaS app.

### 📁 partials

Store reusable snippets in the partials folder. If you’re unsure whether a snippet should be a partial or a component, place it here. Later, if needed, you can move it to the components folder.

To include a partial, use the theme:: namespace. For example:

```php
@include('theme::partials.alert')
```

This works in any file within your theme folder, even when rendering views:

```php
return view('theme::home');
```

> This also works in any file inside your theme folder, so you can use it in the view method **return view('theme::home')**

---

It’s probably helpful to think of your application and each theme in two parts. **Marketing** and the **App**. The **marketing** pages are typically used for **guest** (non-authenticated) users, while the **app** layout is for **authenticated** users.

That is the basic anatomy of a **theme** within Wave. You can utilize all the magical powers of <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a>, <a href="https://livewire.laravel.com/docs/volt" target="_blank">Laravel Volt</a>, and <a href="https://laravel.com/docs/blade" target="_blank">Laravel Blade</a> to create the SaaS you envision.

## Digging Deeper

Visit the <a href="{ url('/docs/guides/creating-themes') }">Creating Themes guide</a> to learn more about how simple it can be to create your own theme. Additionally if you want to source dive you can check out the DevDojo Themes package here.

Next, we'll talk about Volt pages. Because as you can see that each theme also has a `pages` directory. Any file that you place in that directory will automatically be mapped to a route. Let's talk more about that next.