---
title: Static Includes
description: Learn how to use includes to create and re-use HTML code in your website
nextTitle: 'Collections'
nextURL: '/docs/features/collections'
prevTitle: 'Layouts'
prevURL: '/docs/features/layouts' 
---

<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:h-20 md:block" src="/assets/images/icons/includes.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Includes</h1>
      <p class="my-1">Includes allow you to create reusable HTML code snippets and include them in multiple pages of your website.</p>
   </div>
</div>

To use includes, create HTML snippets inside of the **includes** directory. These snippets can then be included in your pages using the `<include src="name-of-file.html"></include>` tags.

## Creating Includes

Creating an include is as simple as adding a new file to the **includes** directory. let's say for instance that you created a new file located at `includes/message.html` with the following contents:

```html
<p>This is a simple HTML paragraph</p>
```

It's as simple as that.

## Using Includes

Next, to use our new include we can utilize the `<include></include>` tags and reference that file, like so:

```html
<!DOCTYPE html>
<html lang="en">
<head>...</head>
<body>
    <include src="message.html"></include>
</body>
</html>
```

Even better we can utilize **layouts** and **includes** together to clean up our code and make it really easy to read:

```html
<layout src="main.html">
    <include src="message.html"></include>
</layout>
```

When this page is rendered, it will have an output like the following:

```html
<!DOCTYPE html>
<html lang="en">
<head>...</head>
<body>
    <p>This is a simple HTML paragraph</p>
</body>
</html>
```

## Include Attributes

You can pass attributes with values to any include. 

```html
<include src="heading.html" title="Welcome to my website"></include>
```

And inside of the include content you can reference the attributes with the curly braces `{}`.

Here's an example. Let's take a look at an example **include** file that can be used as a page heading.

<div class="py-3.5 px-5 font-mono text-xs text-neutral-400 font-bold border rounded-md bg-neutral-950 border-neutral-800">📄 includes/page-heading.html</div>

```html
<div class="relative">
    <h2 class="text-lg">Page Title</h2>
    <p>Description here</p>
</div>
```

Instead of hardcoding the `Page Title` and `Description here`, we could reference `title` and `description` attributes with curly braces, like so:

```html
<div class="relative">
    <h2 class="text-lg">{title}</h2>
    <p>{description}</p>
</div>
```

And when we use the include, we can pass the title and the description as attributes:

```html
<include 
    src="page-heading" 
    title="Contact" 
    description="some description...">
<include>
```

This would render out the following HTML:

```html
<div class="relative">
    <h2 class="text-lg">Contact</h2>
    <p>some description...</p>
</div>
```
<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-purple-600 border-l-4 border-purple-800 rounded-md">
    <img class="w-auto h-12 mr-3.5 my-0" src="/assets/images/icons/book-question.png" />
    <span class="leading-tight opacity-80">Did you know you can also use includes with dynamic attributes inside of Loops. We'll cover loops and ForEach tags in the next section.</span>
</div>

## Organizing Includes

It may be beneficial to group includes into separate folders. For instance, if there are includes that are only going to be used on the homepage, you can group that into a separate folder, like so:

```
📁 includes
├─ 📁 home
├──├─ 📄 hero.html
├──├─ 📄 testimonials.html
```

You can then use these includes by referencing `home/hero.html` inside of the `src` attribute, like so:

```
<layout src="main.html" title="Welcome to our website">
    <include src="home/hero.html"></include>
    <include src="home/testimonials.html"></include>
</layout>
```

> Organizing your includes will make it easier to find them when you want to make updates.

## Conclusion

Includes give us the ability to create HTML snippets in one place and use it in multiple places throughout our site. It will also allow us to make an edit in one place and have those changes replicated everywhere else throughout our website.