---
title: Static Folder Structure
description: Learn about the folder structure in Static and how to organize your files.
nextTitle: null
nextURL: null
prevTitle: 'Deploying Your Site'
prevURL: '/docs/guides/deploy'
---

<div class="flex items-start px-5 py-5 mb-12 md:mb-5 mt-1 md:translate-y-0 translate-y-5 leading-[18px] bg-neutral-950 border border-yellow-400 rounded-md">
   <img class="hidden w-auto h-12 my-0 mr-5 md:block md:h-20" src="/assets/images/icons/folder-structure.png" />
   <div>
      <h1 class="mb-0 text-base md:text-3xl">Folder Structure</h1>
      <p class="my-1">In this section we'll cover the basic folder structure of a Static website. This will help you learn how to organize files or folders appropriately for your project.</p>
   </div>
</div>

## Default Folder Structure

When you create a new **Static** website using the <code>static new</code> command, inside of that new project folder you'll have a new folder/file structure that looks like the following:

```bash
- 📁 assets
- 📁 collections
- 📁 content
- 📁 includes
- 📁 layouts
- 📁 pages
- 📁 public
- 📄 README.md
- 📄 .gitignore
- 📄 tailwind.config.js
```

Let's dive into each folder nad file to understand its contents and purpose.

## The Folders

### Assets Folder
The assets folder is where you store all your static assets such as images, stylesheets, JavaScript files, and fonts. This folder is used to keep your project's resources organized and easily accessible.

### Collections Folder
The collections folder is used to store JSON files that represent collections of data. These collections can be used to dynamically generate content on your website.

### Content Folder
This is where you will create content for your website including posts, articles, and any other type of content. These are stored as Markdown files and will be automatically generated as content pages.

### Includes Folder
The includes folder is used to store reusable components or snippets of code that can be included inside of any pages or layouts.

### Layouts Folder
The layouts folder contains layout templates that define the structure and design of a webpage. Any page on your website can use any layout defined in the layout folder.

### Pages Folder
The pages folder is where you will create pages of your website using the page-based routing system we'll discuss in the next section.

### Public Folder
The public folder is for files that will live at the root folder of your website. This can be anything you want to include like favicons, robots.txt, etc..

## The Files

In addition to the folders mentioned above, there are three files that are typically found at the root of the project:

### README.md
The README.md file is a markdown file that provides an overview of your website. This will show up as the Readme file on your github page.

### .gitignore
The .gitignore file is used to specify which files and folders should be ignored by version control systems like Git.


### tailwind.config.js
This is your Tailwind configuration file. If you are not going to use Tailwind you can remove this file.
