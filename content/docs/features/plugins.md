---
title: Plugins
description: Learn about Wave Plugins
prevTitle: 'Volt'
prevURL: '/docs/features/themes'
nextTitle: null
nextURL: null
---

# Plug-ins

Wave offers a simple way to include additional funcitonality in your app with plug-ins.
- [Plug-ins](#plug-ins)
    - [Plug-in Location](#plug-in-location)
    - [Installed Plug-ins](#installed-plug-ins)
    - [How Plugins Work](#how-plugins-work)
      - [The Plugin Service Provider](#the-plugin-service-provider)
      - [Autoloading](#autoloading)
      - [Plugin Loading Process](#plugin-loading-process)

### Plug-in Location

Plug-ins will be located in the `resources/plugins` folder. Say that we had a plugin called `discussions`, this plugin source would live inside of the `resources/plugins/resources` folder. You'll also see inside of the plugins folder there is an `installed.json` file. This is the file that will contain the installed components. More about this below.

### Installed Plug-ins

You can find all the installed plugins located inside the `resources/plugins/installed.json` file. This will contain an array of installed plugin names. Example, if we had installed the `discussions` package, the contents of the `installed.json` file would look like: 

```json
[
    "Discussions"
]
```

### How Plugins Work

The Wave plugin system is designed to be intuitive for Laravel developers, as it closely mimics the behavior of Laravel service providers. At the core of each plugin is the main plugin file (e.g., `ExamplePlugin.php`), which acts as the entry point and service provider for the plugin.

#### The Plugin Service Provider

The `ExamplePlugin.php` file extends the `Wave\Plugins\Plugin` class, which in turn extends Laravel's `Illuminate\Support\ServiceProvider`. This structure allows plugin developers to utilize the familiar `register` and `boot` methods to add functionality to their plugins.

1. **Register Method**: 
   The `register` method is used to bind things into the service container. This is where you should register services, configuration, and other bindings.

   ```php
   public function register()
   {
       $this->loadViewsFrom(__DIR__ . '/resources/views', 'example');
       $this->mergeConfigFrom(__DIR__ . '/config/example.php', 'example');
   }
   ```

2. **Boot Method**: 
   The `boot` method is called after all services have been registered. It's used for any actions that depend on other services being available.

   ```php
   public function boot()
   {
       $this->loadMigrationsFrom(__DIR__ . '/database/migrations');
       $this->loadRoutesFrom(__DIR__ . '/routes/web.php');
       // Publish assets, config files, etc.
   }
   ```

#### Autoloading

All classes and files inside the `src` folder of the plugin are autoloaded. This means you can easily organize your plugin's code into models, controllers, and other class types without worrying about manually including files.

The autoloading is handled by the plugin system's custom autoloader, which follows PSR-4 standards. For example, a class located at `src/Models/Example.php` would be autoloaded with the namespace `Wave\Plugins\Example\Models\Example`.

#### Plugin Loading Process

1. The Wave application scans the `resources/plugins/installed.json` file to determine which plugins are installed.
2. For each installed plugin, the system instantiates the main plugin class (e.g., `ExamplePlugin`).
3. The `register` method of the plugin is called, allowing it to register its services with the application.
4. After all plugins are registered, the `boot` method of each plugin is called in turn.

This process ensures that plugins can interact with the Wave application just like built-in Laravel service providers, making it easy to extend and enhance the functionality of your Wave application.