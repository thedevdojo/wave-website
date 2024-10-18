---
title: Themes
description: Learn how to use themes
prevTitle: 'Admin'
prevURL: '/docs/features/admin'
nextTitle: 'Plugins'
nextURL: '/docs/features/plugins'
---

# Themes

Wave allows you to customize the look and feel of your application through a flexible and easy-to-use theme system.

- [Themes](#themes)
  - [Theme Views](#theme-views)
  - [Theme Pages](#theme-pages)
  - [Theme Assets](#theme-assets)
    - [Compiling Assets \& HMR](#compiling-assets--hmr)
    - [Building Assets](#building-assets)
    - [How Does It Work](#how-does-it-work)
  - [Selecting Themes](#selecting-themes)
    - [Download Themes](#download-themes)
    - [Installing Themes](#installing-themes)
    - [Activate Theme](#activate-theme)
  - [Theme Structure](#theme-structure)
    - [Readme.md](#readmemd)
    - [theme.jpg](#themejpg)
    - [theme.json](#themejson)
    - [📁 assets](#-assets)
    - [📁 components](#-components)
    - [📁 pages](#-pages)
    - [📁 partials](#-partials)
  - [Digging Deeper](#digging-deeper)


In this section you will learn where the themes are located and how to activate a specific theme.

## Theme Views

All the views that you need for your application will live inside your `resources/themes/{theme}` folder. When you install Wave, the default theme `anchor` is activated. Therefore all you theme files will be located at `resources/themes/anchor`.

The active theme location is registered in the `theme` view namespace, so as an example if you wanted to reference a `home.blade.php` file inside the active theme you can return a view like so:

```php
return view('theme::home');
```

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

### Compiling Assets & HMR

You can use the common `npm run dev` command to compile your assets and serve them up from your current theme. Running `npm run dev` also supports Hot Module Reloading so when you make a change to any theme file, your assets will automatically be compiled and the browser will refresh.

### Building Assets

When you want to build your assets for production you will run `npm run build`. Wave utilizes the same commands that a default Laravel application supports. You may want to learn more about how to customize and modify your asset builder by visiting the <a href="https://laravel.com/docs/vite" target="_blank">Laravel Vite</a> documentation.

### How Does It Work

You may want to know how the asset bundler works in case you need to debug an issue or implement some additional functionality. When you **Activate** a theme, a new file called `theme.json` will be stored in the root of your directory containing something like the following:

```json
{
    "name": "anchor"
}
```

This file stores the currently active theme inside of the `theme.json` file. This will be used inside our `vite.config.js`, file like so:

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

As you can see the `vite` config will read this file to find the currently active theme and then it will compile those assets.

## Selecting Themes

When you want to select a new theme to use, you will need to download and install the specific theme and then you'll need to login to the admin section and activate that theme.

### Download Themes

Visit the <a href="{ url('/themes') }" target="_blank">Themes Page</a> from this website and you'll see a list of available themes to download. Be sure to return to this page often as we'll be releasing many more themes down the road. After you download the theme you'll need to install it (movie the contents).

### Installing Themes

Installing themes are really simple. After you <a href="{ url('/themes') }" target="_blank">download the theme</a> you want to use make sure to extract the theme and move the contents of that folder to the `resources/themes` directory. So, for example if you download the `blank` theme, you should have a new theme folder located at `resources/themes/blank` and all the contents of that theme should be inside that folder.

> You will want to rename the folder to be the name of the theme. As an example if you download the blank theme and it has a folder name of `blank-main`, you'll want to rename it to be `blank`.

### Activate Theme

Now that you have the theme installed, you'll need to head to the admin to activate it. Be sure to login as your admin user and visit <a href="/admin/themes" target="_blank">`/admin/themes`</a> and you’ll see the current themes available in your app.

<img src="https://cdn.devdojo.com/images/august2024/activate-theme.png" class="w-full" alt="Wave Activate Theme" />

To activate a Theme you can simply click the Activate button for the current theme you would like to activate, and that will be the current active theme.

> After activating a theme you may need to make sure that you stop your asset watcher `npm run dev` and re-run it after the new theme has been activated.

## Theme Structure

It's beneficial to know how each theme is structured and organized. Here is the file contents of each theme:

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

```
<x-button>Button Text</x-button>
```

instead of this:

```
<x-elements.button>Button Text</x-elements.button>
```

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