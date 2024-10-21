---
title: Functionality
description: This is a common question that we get with newcomers
prevTitle: 'Local Development'
prevURL: '/docs/local-dev'
nextTitle: 'Upgrading'
nextURL: '/docs/upgrading'
---

# Adding Functionality

If this is your first time using Wave, you may be asking yourself, where do I add my own custom functionality.

## Add Logic Anywhere

This is a typical Laravel application. You can add functionality anywhere you'd like—or in all the familiar places like controllers, models, services, and more. There’s no wrong way to add logic to your application. If it works and you’re happy with the functionality, feel free to keep building however you see fit. You will want to structure your code in a way that keeps everything organized and maintainable for your specific use-case.

## Recommended Approach

Because Wave utilizes Livewire Volt single-file pages, we recommend this structure for adding new functionality. Single-file Livewire Volt pages help streamline your code organization and make future upgrades to Wave more manageable. While this approach simplifies development, you’re completely free to choose how to structure your application based on your preferences and project needs.

If you choose to follow the recommended approach and build your functionality using Volt pages, it can still be beneficial to abstract any complex logic out of the single-file Volt page itself. When the logic becomes lengthy, consider moving it to a service class or controller to keep your code clean and maintainable. This allows you to simplify your Volt page, making it more focused on the user interface while keeping business logic organized and easier to test or extend in the future.

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

