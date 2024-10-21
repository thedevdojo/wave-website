---
title: Your Functionality
description: Where should you add your own logic and functionality within Wave?
prevTitle: 'Local Development'
prevURL: '/docs/local-dev'
nextTitle: 'Upgrading'
nextURL: '/docs/upgrading'
---

# Your Functionality

If this is your first time using Wave, you may be asking yourself, "Where do I add my own logic and functionality". The Answer to that is pretty simple. Anywhere you want, with some considerations.

## Common Practice

Wave is a typical Laravel application, which means you can add functionality in all the familiar places like controllers, models, services, and more. There’s no wrong way to add logic to your application. If it works and you’re happy with it, feel free to keep building however you see fit. You will most-likely want to structure your code in a way that keeps everything organized and maintainable. With that said, we do have a mild recommendation that might help.

## Recommended Approach

Because Wave utilizes Livewire Volt single-file pages, we recommend that you continue to use Single-file Volt pages for adding new functionality. Using Single-file Livewire Volt pages will help keep your code organized and make future upgrades more manageable. While this approach simplifies development, you’re completely free to choose how to structure your application based on your preferences and project needs.

If you choose to follow the recommended approach and build your functionality using Volt pages, it can still be beneficial to abstract any complex logic out of the single-file Volt page itself. When the logic becomes lengthy, consider moving it to a service class or controller to keep your code clean and maintainable. This allows you to simplify your Volt page, making it easier to locate and modify functionality.

## Recommended Example

Say that you want to create a `projects` table and allow your customers to create new projects. You could do this by simply creating a new model:

```
Projects Model
```

And then inside your `resources/themes/theme_name/pages` folder, you can add a new folder called `projects` and inside this folder you'll add an `index.blade.php`. Here is an example of how this page might look.

```

```

As you can see, this page will output all the projects that belong to this specific user.

```
```

Next, perhaps you want to create a way for the user to create a new project, next inside the same `projects` folder, you can add a new file called `create.blade.php`, this might look something like this:

```
create page
```

Now, if you navigate to `app_url.test/projects/create` the authenticated user will be able to create a simple project. They can also visit your application at `app_url.test/projects` to view/edit/delete their existing projects.

This is just an example of how you can add custom logic for your application. Obviously there is no right or wrong way to do this. It is whatever way you feel the most comfortable adding and maintaining the logic in your application.

