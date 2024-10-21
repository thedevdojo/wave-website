---
title: Creating a Plugin
description: Create a plugin using an artisan command
prevTitle: 'Create a Role'
prevURL: '/docs/prompts/create-role' 
nextTitle: 'About Guides'
nextURL: '/docs/guides/about'
---

## Create a Plugin

The `plugin:create` command will create a starting point for you to start building out your own plugin. When you run this command you'll need to specify the name of your plugin, so if you wanted to create a plugin called `hello`, you would run the following command:

```shell
php artisan plugin:create hello
```

You will get a prompt that asks you to enter the description of your plugin:

```bash
Provide a short description for your plugin:
 > A simple hello world plugin example
```

After adding a simple description, your new plugin will be created at `resources/plugins/hello`

## Plugin Contents

When you create a new plugin you'll have a folder structure that looks something like this:

- **HelloPlugin.php**
- **version.json**
- **plugin.jpg**
- routes/**web.php**
- resources/views/**home.blade.php**
- resources/views/livewire/**hello.blade.php**
- src/Components/**Hello.php**

This is just a starting point for your plugin, you can restructure the plugin to contain as many or as few files as you would like. The important file to pay attention to is the **HelloPlugin.php**, this is the entry point for your plugin. You can learn more about that by <a href="{ url('/docs/features/plugins') }">visiting the Plugin page</a>.

## Deleting Plugins

To delete a plugin, you can simple delete the folder from the `resources/plugins` folder. You will also want to make sure that the plug-in is not active; otherwise, you will need to remove it from the `resources/plugins/installed.json` file.

## Renaming Plugins

If you would like to rename a plug-in, you'll need to change the folder name and the corresponding **Plugin.php**, as an example, say that we renamed the `hello` plugin and we wanted to change it to `goodbye`, we would rename the `hello` folder to `goodbye` and the **HelloPlugin.php** to **GoodbyePlugin.php**. You will also change the name of the class inside that file, and you may need to change references in the **Plugin.php** to correspond with the new name of the new plugin.

Next, you'll need to change the `public $name` inside of the **GoodbyePlugin.php**. You may also want to change the `$description` in that file as well:

```php
<?php

...

class GoodbyePlugin extends Plugin
{
    protected $name = 'Goodbye';

    protected $description = 'This is where you would change the description';

...
```

## Sharing Plugins

You can feel free to share or re-use plugins inside of any application. We currently do not have a place where other users can find community generated plug-ins, but if the demand is there, we'll definitely consider adding a place for it.

---

To learn more about plugins, visit the <a href="{ url('/docs/features/plugins') }">Plugin Feature page</a>.



