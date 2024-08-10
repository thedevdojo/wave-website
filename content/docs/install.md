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

To download a fresh copy of Wave, click the download button below.<span class="hidden">You can also find links to all <a href="https://github.com/thedevdojo/wave/tags" target="_blank">versions here</a>.</span>

<div class="flex relative justify-start items-start">
<div class="flex overflow-hidden relative justify-center items-center p-1 mb-5 rounded-full border border-gray-200 duration-300 ease-out group">
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 w-[250px] rounded-full group-hover:opacity-100 opacity-0 blur-sm duration-300 ease-out scale-100 h-[250px] -translate-y-1/2 origin-center">
        <span class="absolute inset-0 w-full h-full bg-gradient-to-r from-indigo-500 via-teal-300 to-blue-500 rounded-full group-hover:animate-spin-slow"></span>
    </div>
    
    <a href="/wave/download" class="inline-block relative z-20 flex-shrink-0 px-6 py-3 w-full text-sm font-bold text-center text-white no-underline bg-gray-900 rounded-full shadow-xl sm:w-auto hover:bg-gray-950">Download Wave V3</a>
</div>
</div>



After downloading, follow these steps to finish the installation:

1. Unzip the downloaded file.
2. Rename the unzipped folder to any name you prefer.
3. Move the renamed folder to one of your <a href="https://herd.laravel.com/docs/1/getting-started/sites" target="_blank">site directories</a>. For example, you can move it to `~/Herd`.
4. Open your browser and visit `foldername.test` to start the installation process. Remember to replace `foldername` with the actual name of the folder.

> 🎉 That’s it! Wave is now installed. If you encounter any errors during the automated installer, continue reading; otherwise, skip to the **Database** section

---

If receive an error when trying to run through the automated installer, you may need to run the following commands from your project folder:

<div class="p-5 font-mono text-sm bg-gray-800 rounded-xl leading-[24px] whitespace-break-spaces"><span class="text-[#62d6e8]">cp</span> <span class="text-[#f8e164]">.env.example</span> <span class="text-[#f8e164]">.env</span>&nbsp;
<span class="text-[#62d6e8]">composer</span> <span class="text-[#f8e164]">install</span></div>

Then, visit the project URL in the browser to finish the installation.

## Database

By default Wave uses an `SQLite` connection stored at `database/database.sqlite`. If you wish, you can change this connection from inside your `.env` file. As an example, this is how a MySQL connection will look: 

```ini
CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=database-name
DB_USERNAME=root
DB_PASSWORD=''
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