---
title: Blog
description: Learn how to use the blog
prevTitle: 'Changelog'
prevURL: '/docs/features/changelog'
nextTitle: 'Pages'
nextURL: '/docs/features/pages'
---

# Blog

An easy way to get traffic to your SaaS is to have a blog. When you write about relevant content related to your SaaS you will widen your net of getting new users to signup for on your app.

In this section you will learn about the blogging feature that comes along with Wave.

- [Blog](#blog)
    - [Your Blog](#your-blog)
    - [Posts Admin](#posts-admin)
    - [Post Categories](#post-categories)

---

### Your Blog

After installing Wave, you will have a blog located at the `/blog` route. You can modify or edit this view file located at `resources/themes/{theme_folder}/blog/index.blade.php`

<img src="https://cdn.devdojo.com/images/august2024/blog.png" alt="Blog" class="w-full" />

You can also view a single post by clicking the thumbnail or title of the post. The individual post view is at `resources/themes/{theme_folder}/blog/[.Wave.Category-slug]/[.Wave.Post-slug].blade.php`

<img src="https://cdn.devdojo.com/images/august2024/blog-post.png" alt="Blog Post" class="w-full" />

### Posts Admin

You can edit, add, or delete posts in your admin by visiting the `/admin/posts`. To create a new post you can click the `New post` button:

<img src="https://cdn.devdojo.com/images/august2024/posts.png" alt="Posts" class="w-full" />

Then, you'll need to fill out your new post information and click save. Only Posts with a status of `PUBLISHED` will show up on the front-end.

<img src="https://cdn.devdojo.com/images/august2024/post-create.png" alt="Post Create" class="w-full" />

### Post Categories

You can also choose to Add, Edit or Delete post categories by visiting the Admin Post Categories at `/admin/categories`. When you click `New category` you'll see a new page where you can add a custom category.

<img src="https://cdn.devdojo.com/images/august2024/category-create.png" alt="Category Create" class="w-full" />

After adding a new category, you will be able to create a new post and categorize it in that specific category.
