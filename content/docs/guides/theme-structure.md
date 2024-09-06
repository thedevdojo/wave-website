---
title: Structure of a Wave Theme
description: Learn about the structure of a Wave theme
nextTitle: ''
nextURL: null
prevTitle: 'Creating Themes'
prevURL: '/docs/guides/creating-themes' 
---

# Creating Themes

In this guide, you will learn about the structure and architecture of a theme folder/file system in Wave.

- [Creating Themes](#creating-themes)
    - [Files and Folders](#files-and-folders)
    - [Explanation of Files](#explanation-of-files)
  - [Assets Folder](#assets-folder)
  - [Components Folder](#components-folder)
    - [components/app folder](#componentsapp-folder)
  - [components/elements folder](#componentselements-folder)
    - [components/marketing folder](#componentsmarketing-folder)
    - [components/layouts folder](#componentslayouts-folder)
  - [Pages Folder](#pages-folder)
  - [Partials Folder](#partials-folder)


**Important Note**: Each theme contains two layouts: **app** and **marketing**, located in the `{theme_folder}/components/layouts` folder. It’s recommended to think of your application in these two parts. The **marketing** layout is for **guest** (non-authenticated) users, while the **app** layout is for **authenticated** users.

While this structure isn’t mandatory, all themes are designed this way for better organization.

### Files and Folders

Each theme includes the following:

 - **assets (folder)**
 - **components (folder)**
 - **pages (folder)**
 - **partials (folder)**
 - Readme.md
 - theme.jpg
 - theme.json

### Explanation of Files

- **Readme.md**: Contains details about the theme, including installation instructions, links, and other relevant info.
- **theme.jpg**: The cover art image that displays in the admin theme section.
- **theme.json**: This file holds the name and current version of the theme.

Now, let’s dive into the purpose of each folder.

## Assets Folder

The **assets** folder houses your CSS and JavaScript files. By default, it includes:

- `css/app.css`
- `js/app.js`

You can add custom CSS or JS to these files, and they will be automatically included in your application.

## Components Folder

The **components** folder contains reusable components for your theme. It includes four subfolders:

- **app**
- **elements**
- **layouts**
- **marketing**

### components/app folder

Store components specific to your **app** (non-marketing pages) here. 

For example, in the <a href="https://github.com/thedevdojo/example" target="_blank">Example theme</a>, the **components/app** folder contains a **header.blade.php** file used in the app layout.

In this folder you'll want to store any specific components that will be used throughout your **app** (non-marketing pages). 

> For instance, in the <a href="https://github.com/thedevdojo/example" target="_blank">Example theme</a> the **components/app** folder contains a **header.blade.php** file. This is the header element that is used in your **app** layout.

## components/elements folder

This folder contains shared components that can be used throughout your application. Components inside this folder don’t need the `elements` prefix. For instance:

```
<x-button>Button Text</x-button>
```

…instead of:

```
<x-elements.button>Button Text</x-elements.button>
```

### components/marketing folder

This folder holds components used on marketing pages, such as headers, hero sections, features, and more.

### components/layouts folder 

This folder contains your app’s layouts. Every theme comes with two layouts:

 - **app.blade.php** (for authenticated users)
 - **marketing.blade.php** (for guest users)


## Pages Folder

The pages folder is mapped directly to routes via <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a>. For example:

- pages/index.blade.php => **url.com**
- pages/dashboard/index.blade.php => **url.com/dashboard**
- pages/pricing/index.blade.php => **url.com/pricing**
- pages/profile/[username].blade.php => **url.com/profile/johndoe**

... etc.

You can also leverage <a href="https://laravel.com/docs/folio#route-parameters" target="_blank">Route Parameters</a>, <a href="https://laravel.com/docs/folio#route-model-binding" target="_blank">Route Model Binding</a> with Folio.

Additionally, these files support creating single-file <a href="https://livewire.laravel.com/docs/volt" target="_blank">Volt components</a> by adding logic at the top of the view and using the **@volt** directive. Learn <a href="{ url('/docs/features/volt') }">more about that here</a>.

The **pages** folder is where you’ll spend a lot of time adding logic to your SaaS app.

## Partials Folder

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

That is the basic anatomy of a **theme** within Wave. You can utilize all the magical powers of <a href="https://laravel.com/docs/folio" target="_blank">Laravel Folio</a>, <a href="https://livewire.laravel.com/docs/volt" target="_blank">Laravel Volt</a>, and <a href="https://laravel.com/docs/blade" target="_blank">Laravel Blade</a> to create the SaaS you envision.