---
title: Static Collections
description: Learn how to add collections of data to your Static website
nextTitle: 'Content'
nextURL: '/docs/features/content'
prevTitle: 'Includes'
prevURL: '/docs/features/includes' 
---

<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="w-auto h-12 my-0 mr-5 md:h-20 md:block hidden" src="/assets/images/icons/collections.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Collections</h1>
      <p class="my-1">Collections allow you to add and manage sets of data in your application. They provide a convenient way to organize and loop through data.</p>
   </div>
</div>

## About Collections

Collections can be used to loop through a collection of data, such as navigation items, product features, or any other type of repeatable data.

<div class="flex items-center px-4 py-4 my-6 leading-[18px] bg-blue-600 border-l-4 border-blue-800 rounded-md">
    <img class="w-auto h-8 mr-3.5 my-0" src="/assets/images/icons/info.png" />
    <span>Collections are stored in the <strong>collections</strong> folder. Don't see the collections folder? Simply create a new folder called <strong>collections</strong> in the root of your project.</span>
</div>


## Creating Collections

Creating a new collection is as simple as creating a new `.json` file to your `collections` folder. The content should be structured as an array of JSON  data. Here's an example.

<div class="py-3.5 px-5 font-mono text-xs text-neutral-400 font-bold border rounded-md bg-neutral-950 border-neutral-800">📄 collections/menu.json</div>

```
[
    {
        "title" : "Home",
        "link" : "/"
    },
    {
        "title" : "About",
        "link" : "/about"
    }
]
```

You can add as many collections to your website and reference that data on your website. You can reference any collection inside of a **collection loop**. Let's cover that next.

## Collection Loops

To loop through a collection we can use the `<ForEach></ForEach>` tags. To reference a collection, you pass the filename inside the `collection` attribute, like so:

```html
<ForEach collection="menu">...</ForEach>
```

To loop through the **collections/menu.json** file, our code might look like this:

```html
<nav>
    <ForEach collection="menu">
        <a href="{menu.link}">{menu.title}</a>
    </ForEach>
</nav>
```

This loop will generate the following HTML:

```
<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
</nav>
```

## Collection Loop Attributes

In addition to the `collection` attribute there are also a few other attributes you can use in the `<ForEach></ForEach>` tags, which include the following:

- **as** - specify how you want to reference the data
- **orderBy** - specify how you want to order the content
- **count** - specify how many items you want to retrieve

To show you an example of these attributes, let's use another collection example.

<div class="py-3.5 px-5 font-mono text-xs text-neutral-400 font-bold border rounded-md bg-neutral-950 border-neutral-800">📄 collections/movies.json</div>

```
```
[
    {
        "title": "Teenage Mutant Ninja Turtles",
        "year" : "1990",
        "active": true
    },
    {
        "title": "The Goonies",
        "year" : "1985",
        "active": false,
    },
    {
        "title": "Batman Forever",
        "year" : "1995",
        "active": true
    },
    {
        "title": "Jurrasic Park",
        "year": "1993",
        "active": false
    }
]
```

If we wanted to loop through our **movies** collection, we can do so with the following code:

```html
<ForEach content="movies" as="movie" orderBy="year" count="3">
    <h2>{movie.title}</h2>
</ForEach>
```

Here we referenced the **movies** collection, and referenced the data as **movie**. We've also specified that we want to retrieve three results and order by the year, resulting in the following output:

```html
<h2>The Goonies</h2>
<h2>Teenage Mutant Ninja Turtles</h2>
<h2>Jurrasic Park</h2>
```

Next, if we want to hide or show data from any collection. We can do that with <strong>conditionals</strong>.

## Conditionals

Inside a loop we can use the `<If></If>` tags to show/hide items based on a specific condition. Using our **movies** collection from above, we can output only `active` movies with the following HTML:

```html
<ul>
    <ForEach collection="movies" as="movie">
        <If condition="movie.active == true">
            <li>{movie.title}</li>
        </If>
    </ForEach>
</ul>

```

This will render the following HTML:

```html
<ul>
    <li>Teenage Mutant Ninja Turtles</li>
    <li>Batman Forever</li>
</ul>
```

When rendering a loop there are times when you want to keep track of the current iteration, we can do that by using the **loop variable**.

## Loop Variable

Inside of any `<ForEach></ForEach>` loop you can utilize the **loop** variable inside of conditional, like so:

```html
<ul>
    <ForEach collection="movies" as="movie">
        <If condition="loop == 2 || loop == 4">
            <li>{movie.title}</li>
        </If>
    </ForEach>
</ul>
```

This will render the following HTML:

```html
<ul>
    <li>The Goonies</li>
    <li>Jurassic Park</li>
</ul>
```

The **loop** variable will start at **1** and it will increment each time the loop iterates.

## Conclusion

Collections are a powerful feature that allow you to organize and loop through sets of data in your static website. If you want to create long copy **text** such as posts or articles, you'll probably want to use Statics **content** feature for that. Let's discuss that next.