---
title: Installing Wave
description: Learn how to install Wave
prevTitle: 'Getting Started'
prevURL: '/docs/getting-started'
nextTitle: 'Local Development'
nextURL: '/docs/local-dev'
---

# Installing Wave

To install Wave you will need a local PHP development environment setup on your machine. The easiest way to do this is by downloading and installing <a href="https://herd.laravel.com" target="_blank">Laravel Herd</a>. After you have done that, we can move on to the next step and download Wave.

## Download Wave

To download a fresh copy of Wave, click the download button below.<span class="hidden">You can also find links to all <a href="https://github.com/thedevdojo/wave/tags" target="_blank">versions here</a>.</span>

<div class="relative flex items-start justify-start w-full sm:w-auto">
<div class="relative flex items-center justify-center w-full p-1 mb-5 overflow-hidden duration-300 ease-out border rounded-lg sm:w-auto sm:rounded-full border-neutral-200 dark:border-neutral-800 group">
    <div class="absolute sm:block hidden top-1/2 left-1/2 -translate-x-1/2 w-[250px] rounded-lg sm:rounded-full group-hover:opacity-100 opacity-0 blur-xs duration-300 ease-out scale-100 h-[250px] -translate-y-1/2 origin-center">
        <span class="absolute inset-0 w-full h-full rounded-lg sm:rounded-full bg-linear-to-r from-indigo-500 via-teal-300 to-blue-500 group-hover:animate-spin-slow"></span>
    </div>
    
    <a href="/wave/download" class="relative shrink-0 inline-block w-full px-6 py-3 text-sm font-bold text-center text-white no-underline rounded-md shadow-xl sm:rounded-full bg-neutral-900 dark:text-neutral-900 dark:bg-neutral-100 dark:hover:bg-white sm:w-auto hover:bg-neutral-950">Download Wave V3</a>
</div>
</div>

After downloading Wave, you have two installation options. If you’re using Herd, select the **Automated Installer**. Otherwise, proceed with the **Manual Installation**.

## Automated Installation with Herd

If you are using <a href="https://herd.laravel.com" target="_blank">Herd</a> to host your sites locally, you can follow these steps to finish the installation via the automated installer:

1. Unzip the downloaded file.
2. Rename the unzipped folder to any name you prefer.
3. Move the renamed folder to one of your <a href="https://herd.laravel.com/docs/1/getting-started/sites" target="_blank">site directories</a>. For example, you can move it to `~/Herd`.
4. Open your browser and visit `foldername.test` to start the installation process. Remember to replace `foldername` with the actual name of the folder.

> That's it! Wave is now installed. If you encounter any errors during the automated installer, you may follow the steps to manually install below; otherwise, move on to the Database section.

## Manual Installation

If you are hosting your Laravel projects locally with something other than Herd, or if you receive an error during the automated installer, you may want to manually install Wave. To do so, continue reading.

Download Wave and unzip the file. Next, move the folder to your sites folder, and follow these steps:

### 1. Copy .env.example file

From inside the project folder, run the following command:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>
```bash
cp .env.example .env
```
</div>

### 2. Install Composer Dependencies

Next, we need to install the composer dependencies:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>
```bash
composer install
```
</div>

### 3. Database Migrations and Seed

Next, we need to migrate and seed the database:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>
```bash
php artisan migrate
php artisan db:seed
```
</div>

> Wave has now been installed. Raise the anchor, man the helm, and prepare for the voyage ahead!

## Database

By default Wave uses an `SQLite` connection stored at `database/database.sqlite`. If you wish, you can change this connection from inside your `.env` file. As an example, this is how a MySQL connection will look: 

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file=".env"></include>

```ini
CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=database-name
DB_USERNAME=root
DB_PASSWORD=''
```
</div>

In most cases `SQLite` will work totally fine.

<a name="login"></a>
## Logging into your Application

After installing Wave, you should automatically be logged in as the admin user. If you need to log in again, you can use the following credentials:

- **email**: admin@admin.com
- **password**: password

Once you've logged in, you can modify the admin email, username, and password by accessing the settings section within the user menu.

---

Next, we'll cover a few more local development commands.