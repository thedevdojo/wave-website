---
title: Upgrading Wave
description: Learn how to upgrade Wave
prevTitle: 'Your Functionality'
prevURL: '/docs/your-functionality'
nextTitle: 'Authentication'
nextURL: '/docs/features/auth'
---

# Upgrading

Upgrading Wave is very simple. Follow the steps below to upgrade.

- [Upgrading](#upgrading)
  - [Automated Upgrade](#automated-upgrade)
  - [How To Upgrade](#how-to-upgrade)
    - [Upgrade Steps](#upgrade-steps)
    - [Theme Upgrade](#theme-upgrade)

---

## Automated Upgrade

We are currently working on an automated upgrade process that will happen directly inside the admin. This will be an automated upgrade similar to that of WordPress and other popular CMS frameworks.

## How To Upgrade

Until the automated upgrade is complete, you will have to upgrade manually by following the steps below.

### Upgrade Steps

Download a copy of the latest version. In the root folder you should see another folder named `wave`, you can simply replace this folder with the `wave` folder in your project. You will also need to replace the folder located at `app/Filament`. If you have made some updates to the admin panel, you will need to make sure to port those changes over (we're currently working on a better way to upgrade the admin functionality).

Next, you will need to re-autoload your dependencies by running:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```bash
composer dump-autoload
```

</div>

You may also need to clear the cache by running:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```bash
php artisan cache:clear
```

</div>

And you should be updated to the latest version :)

### Theme Upgrade

Upgrading the core of Wave is very simple; however, upgrading your current theme may be a bit more complicated based on the modifications you have made.

Typically you will not need to upgrade your theme, it will have all base features and you can build on top of those. If there is a new feature that gets released which has corresponding views, then you may have a few files that you need to manually move into your project.