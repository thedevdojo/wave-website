---
title: Static Layouts
description: Learn how to use layouts to give pages a re-usable HTML structure
nextTitle: 'Includes'
nextURL: '/docs/features/includes'
prevTitle: 'Page-based Routing'
prevURL: '/docs/features/page-based-routing' 
---


<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:h-20 md:block" src="/assets/images/icons/layouts.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Layouts</h1>
      <p class="my-1">Layouts are used to provide a reusable HTML structure for pages. They allow you to define a common layout that can be inherited by multiple pages.</p>
   </div>
</div>

## Creating Layouts

Creating a layout for your application is as simple as creating a `.html` file inside of the `layouts` directory. Here is an example layout:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{title}</title>
    <link rel="icon" type="image/x-icon" href="/assets/images/favicon.png">
    {tailwindcss}
</head>
<body>
    {slot}
    <script src="/assets/js/main.js"></script>
</body>
</html>
```

A layout is an HTML structure that can be used within any page by using the `<layout></layout>` tag. Anything inside the **layout** tags will be rendered in place of the `{slot}` shortcode.

## Using Layouts

Any page inside the `pages` directory can utilize any layout. For instance, let's say that we had a page located at `pages/about.html` with the following contents:

```
<layout src="main.html" title="About Us">
    <h1>About Us</h1>
    <p>Here is some info about us</p>
</layout>
```

Inside of the layout tags we add a `src` of `main.html`, which will load a layout located at `layouts/main.html`. When this `about` page gets rendered it will have the following HTML output:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>About Us</title>
    <link rel="icon" type="image/x-icon" href="/assets/images/favicon.png">
    <!-- TailwindCSS Classes -->
</head>
<body>
    <h1>About Us</h1>
    <p>Here is some info about us</p>
    <script src="/assets/js/main.js"></script>
</body>
</html>
```

> You've probably also noticed the `title` attribute in the <strong>layout</strong> tags. Let's cover that next.

## Layout Variables

When you utilize a `<layout>` from inside a page, you can pass it any set of attributes like `title`, `description`, and any other value you want to reference as a variable inside the layout. If we used a layout inside of a page that looked like this:

```
<layout src="post.html" title="Title" description="my description">
    ...
</layout>
```

Then, inside of that `post.html` layout file you can retrieve those values by referencing the attributes inside of `{}` curly braces. So, if you want to output the value from the *title** attribute you would use `{title}` or to get the description you would use `{description}`.

You can make use of any number of attributes you would like and reference them inside of your layout.

## Conclusion

Layouts make it really simple for multiple pages to inherit a similar layout. It also gives you the ability to have different layouts for different parts of your website.