---
title: Themes
description: Learn how to use themes
prevTitle: 'Admin'
prevURL: '/docs/features/admin'
nextTitle: null
nextURL: null
---

# Themes

Wave has Theme support, which means that when you start a new project you may choose between a few themes to get your application up and running. This also means that you can choose to create different versions of your theme and swap between these different versions by activating and de-activating specific versions.

In this section you will learn where the themes are located and how to activate a specific theme.

## Theme Location

Every theme is located inside of the `resources/themes` folder. When you install Wave there will be 1 theme available, which is the anchor theme. In each theme you will find a `theme.json` file which contains the name of the theme as well as the specific version, like so:

```json
{
	"name": "Anchor",
	"version": "1.0"
}
```

### Creating a Theme

### Downloading a Theme

## Theme Assets

To compile a theme's assets you can navigate into the theme folder and run `npm install`, after you install the node dependencies you can run `npm run watch` to start your asset watcher and develop your theme. When you are ready to compile and minify your assets for production you will want to run `npm run production`.

## Activating Themes

If you are logged in as an admin user and you visit visit the <a href="/admin/themes" target="_blank">`/admin/themes`</a> section of your application you’ll see the current themes available in your app.

![themes](https://cdn.devdojo.com/images/may2021/themes.png)

To activate a Theme you can simply click the Activate button for the current theme you would like to activate, and that will be the current active theme.


For more information on customizing and modifying themes, you may want to check out the <a href="https://devdojo.com/wave/videos" target="_blank">Wave Videos</a> to learn more about how you can customize and build new themes for your application.