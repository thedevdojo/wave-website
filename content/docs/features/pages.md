---
title: Pages
description: Learn about creating and editing pages
prevTitle: 'Blog'
prevURL: '/docs/features/blog'
nextTitle: 'API'
nextURL: '/docs/features/api'
---

# Pages

Wave makes it easy to add a pages via the admin and have it show up on your site. 

> Not to be confused this with <a href="{ url('/docs/features/volt') }">Volt Pages</a>, which are dynamic pages created inside your theme `pages` directory. <a href="{ url('/docs/concepts/volt') }">Learn more about those pages here</a>

These pages in this section are content pages, such as a Terms or Privacy Policy page, or even an About Us page. These pages typically contain static content, and not much dynamic functionality or user interaction.

- [Pages](#pages)
  - [Creating Pages](#creating-pages)
  - [Page View](#page-view)
  - [Which to Use](#which-to-use)

---

## Creating Pages

If you visit your website `/admin/pages` directory, you'll see a few example pages.

<img src="https://cdn.devdojo.com/images/october2024/admin-pages.png" class="w-full" />

You can click on the **New page** button to create a new page.

<img src="https://cdn.devdojo.com/images/october2024/create-page.png" class="w-full" />

After creating a new page, this route will automatically be available on your site. If you created a page with the **slug** of `hello-world` you will see a new route on your webiste at `/hello-world`.

## Page View

You can modify the pages view by modifying the file inside of `resources/themes/theme_name/page.blade.php`. When a page is rendered on your website it will use this view to output the content.

## Which to Use

You might be wondering when to create a page through the admin panel versus adding a new page inside of your themes `pages` directory. The choice is entirely yours, but here are a few considerations to help you decide

**Pages via Admin** - These are ideal for simple content pages like a Privacy Policy or Terms of Service. This allows you to quickly edit content and see changes instantly.

**Pages via Pages Folder** - Perfect for pages requiring a unique layout, custom logic, or additional styling. This option provides more control over design and functionality.
