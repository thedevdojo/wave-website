---
title: Installing Wave
description: Learn how to install Wave
prevTitle: 'Getting Started'
prevURL: '/docs/getting-started'
nextTitle: 'Local Development'
nextURL: '/docs/local-dev'
---

# Installing Wave

Before installation you need a local PHP development environment. The easiest way to do this is to download and install <a href="https://herd.laravel.com" target="_blank">Laravel Herd</a>. Once your local environment is set up, we can move on to the next step and download Wave.

## Download Wave

To download a fresh copy of Wave, click the button below. You can also find download links to all <a href="https://github.com/thedevdojo/wave/tags" target="_blank">versions here</a>.

<a href="/wave/download" class="inline-block flex-shrink-0 px-6 py-3 mb-5 w-full text-sm font-bold text-center text-white no-underline bg-gray-900 rounded-full shadow-xl sm:w-auto hover:bg-gray-950">Download Wave V3</a>

After downloading, follow these steps to finish the installation:

1. Unzip the downloaded file.
2. Rename the unzipped folder to any name you prefer.
3. Move the renamed folder to one of your <a href="https://herd.laravel.com/docs/1/getting-started/sites" target="_blank">site directories</a>. For example, you can move it to `~/Herd`.
4. Open your browser and visit `foldername.test` to start the installation process. Remember to replace `foldername` with the actual name of the folder.

> 🎉 That’s it! Wave is now installed. If you encounter any errors during the automated installer, continue reading; otherwise, skip to the **Database** section

---

If receive an error when trying to run through the automated installer, you may need to run the following commands from your project folder:

```bash
cp .env.example .env
composer install
```

Then, visit the project URL in the browser to finish the installation.

## Database

By default Wave uses an `SQLite` connection stored at `database/database.sqlite`. If you wish, you can change this connection from inside your `.env` file. As an example, this is how a MySQL connection will look: 

```bash
CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=database-name
DB_USERNAME=root
DB_PASSWORD=
```

In most cases `SQLite` will work totally fine.

<a name="login"></a>
## Logging into your Application

After installing Wave, you should automatically be logged in as the admin user. If you need to log in again, you can use the following credentials:

- **email**: admin@admin.com
- **password**: password

Once you've logged in, you can modify the admin email, username, and password by accessing the settings section within the user menu.

---

Next, we'll cover a few more local development commands.