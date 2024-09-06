---
title: Structure of a Wave Theme
description: Learn about the structure of a Wave theme
nextTitle: ''
nextURL: null
prevTitle: 'Creating Themes'
prevURL: '/docs/guides/creating-themes' 
---

# Creating Themes

In this guide you will learn about the structure and architecture of a theme folder/file system.

- [Creating Themes](#creating-themes)
    - [Files and Folders](#files-and-folders)
  - [Assets Folder](#assets-folder)
  - [Components Folder](#components-folder)
    - [components/app folder](#componentsapp-folder)
  - [components/elements folder](#componentselements-folder)
    - [components/marketing folder](#componentsmarketing-folder)
    - [components/layouts folder](#componentslayouts-folder)
  - [Pages Folder](#pages-folder)
  - [Partials Folder](#partials-folder)


**Important Note**: Each theme contains two layouts, **app** and **marketing**, located in the `{theme_folder}/components/layouts` folder. It's often better for organization purposes if you think of your application in these two parts. Marketing is the layout that will be used for **guest** (non-authenticated) users in your application, and the **App** layout will be used by **authenticated** users in your application.

It's not mandatory that you structure your app this way; however, every theme is designed this way for better organization.

### Files and Folders

 - **assets (folder)**
 - **components (folder)**
 - **pages (folder)**
 - **partials (folder)**
 - Readme.md
 - theme.jpg
 - theme.json

Each theme will have four folders and three files. Each of the files are pretty self explanatory; however, we'll describe them briefly below:

- Readme.md - This file will contain information about the them including additional install instructions, links, and other relevant info you may need to understand for each theme.
- theme.jpg - This is the cover art image that will show in the admin theme section.
- theme.json - This file will contain the name and current version of the theme.

Next, we'll cover each folder and it's purpose.

## Assets Folder

The assets folder will contain your **CSS** or **Javascript** files. You'll see that inside this folder there are already two files which include the `css/app.css` and the `js/app.js` file.

You can add any custom CSS or JS to these files and it will automatically be included in your application.

## Components Folder

This file contains many of the components you will use throughout your theme. Inside this theme there are four additional folder which include the **app**, **elements**, **layouts**, and **marketing**.

### components/app folder

In this folder you'll want to store any specific components that will be used throughout your **app** (non-marketing pages). 

> For instance, in the <a href="https://github.com/thedevdojo/example" target="_blank">Example theme</a> the **components/app** folder contains a **header.blade.php** file. This is the header element that is used in your **app** layout.

## components/elements folder

This folder contains any shared components that you will use throughout your application. This folder is mapped directly to the blade component without needing the `elements` prefix. As an example if you had a file called `button.blade.php` inside of this folder, you do not need to write it like so:

```
<x-elements.button>Button Text</x-elements.button>
```

Instead you can simply write it like so:

```
<x-button>Button Text</x-button>
```

Store all your re-usable elements in this folder.

### components/marketing folder

This folder contains components that will be used for your marketing pages. It will also contain a header element specific for marketing pages. It will also include common sections such as `heros`, `features`, and more.

### components/layouts folder 

This folder contains all the layouts that you want to use in your application. As we explained at the beginning of this guide, your theme will come with an **app** layout (authenticated user) and a **guest** layout (guest users).

## Pages Folder

This folder is mounted as a <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a> folder, which means that every file in this folder is mapped to a route.

- pages/index.blade.php => **url.com**
- pages/dashboard/index.blade.php => **url.com/dashboard**
- pages/pricing/index.blade.php => **url.com/pricing**
- pages/profile/[username].blade.php => **url.com/profile/johndoe**

... etc.

You can enjoy <a href="https://laravel.com/docs/folio#route-parameters" target="_blank">Route Parameters</a>, <a href="https://laravel.com/docs/folio#route-model-binding" target="_blank">Route Model Binding</a>, and all the other luxuries of <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a>.

In each of these files you can also creating single file <a href="https://livewire.laravel.com/docs/volt" target="_blank">Volt components</a> by simply adding logic to the top of the view and utilizing the **@volt** directive. Learn <a href="{ url('/docs/features/volt') }">more about that here</a>.

The pages folder is very important and is probably where you will be creating most of your files in order to add more logic to your SaaS.

## Partials Folder

This folder contains any partials that you want to re-use in your views. If you are unsure whether a snippet should be a partial or a component, just store it in the `partials` folder and if you need additional functionality later, add it in the components folder.

When you render a partial, you can utilize the `theme::` namespace, so when you include a file, you can use the following syntax:

```
@include('theme::partials.alert')
```

> This also works in any file inside your theme folder, so you can use it in the view method **return view('theme::home')**

---

That is the basic anatomy of a **theme** within Wave. You can utilize all the magical powers of <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a>, <a href="https://livewire.laravel.com/docs/volt" target="_blank">Laravel Volt</a>, and <a href="https://laravel.com/docs/blade" target="_blank">Laravel Blade</a>, so feel free to use them however you would like in order to create the SaaS you invision.