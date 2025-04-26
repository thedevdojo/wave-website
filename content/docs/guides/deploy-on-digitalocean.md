---
title: Deploying Wave to DigitalOcean
description: Learn how to deploy Wave to DigitalOcean using the Laravel One-Click Droplet.
prevTitle: 'Using Filament With Volt'
prevURL: '/docs/guides/using-filament-with-volt'
nextTitle: ''
nextURL: null
---

# Deploying Wave to DigitalOcean

Wave can be deployed seamlessly using DigitalOcean's Laravel One-Click Droplet. The Laravel One-Click app provides a pre-configured environment, saving time and effort when setting up your project.

---

## Prerequisites

Before you begin, ensure you have:

- A [DigitalOcean account](https://m.do.co/c/dc19b9819d06).
- A registered domain name (optional but recommended for SSL).
- Basic familiarity with SSH and terminal commands.

---

## Step 1: Create the Laravel One-Click Droplet

1. Navigate to the [Laravel One-Click Marketplace listing](https://marketplace.digitalocean.com/apps/laravel).
2. Click **Create Laravel Droplet** and configure:
    - Choose a plan (Basic, General Purpose, or Premium).
    - Select a data center region close to your target audience.
    - Recomended, enable backups for added security.

3. Complete the creation process and note the public IPv4 address of the Droplet.

---

## Step 2: Log Into Your Droplet

1. Open your terminal and SSH into the Droplet:

    ```bash
    ssh root@your_droplet_public_ipv4
    ```

2. If prompted, set a new password or confirm your SSH key.

---

## Step 3: Configure Your Domain (Optional)

During the initial setup, the interactive script will prompt you for your domain or subdomain. Enter your domain (e.g., `example.com`) and proceed.

To ensure proper domain resolution, configure DNS records for your domain:
- **A Record**: `example.com` -> `your_droplet_public_ipv4`
- **A Record**: `www.example.com` -> `your_droplet_public_ipv4`

---

## Step 4: Enable SSL (Recommended)

You will be prompted to enable SSL via Let's Encrypt. If you've pointed your domain to the Droplet's IP address, choose `y` to enable SSL. This secures your site with HTTPS.

---

## Step 5: Download and Set Up Wave

1. **Access the Droplet**:

    Once connected to the Droplet, you will be in the `/root` directory.

    Switch to the `larasail` user:

    ```bash
    su larasail
    ```

    Change to the web root:

    ```bash
    cd /var/www/
    ```

2. **Download Wave**:
    Replace the existing Laravel project with Wave. First, back up the existing project:

    ```bash
    mv /var/www/laravel /var/www/laravel_backup
    ```

    Clone Wave from GitHub:

    ```bash
    git clone git@github.com:thedevdojo/wave.git laravel
    ```

    Change the `thedevedojo` to your GitHub username if you forked the repository.

    Then update the permissions for the storage directory so that the web server can write to it and store temporary files:

    ```bash
    sudo chown -R larasail:www-data /var/www/laravel/storage
    ```

3. **Install Dependencies**:

    Access the `/var/www/laravel` directory:

    ```bash
    cd /var/www/laravel
    ```

    Inside the `/var/www/laravel` directory, run:

    ```bash
    composer install
    ```

4. **Environment Configuration**:
    Copy and configure the `.env` file:

    ```bash
    cp .env.example .env
    nano .env
    ```

    You can use a SQLite database or configure MySQL database. You can create a database and user for it by using the following command:

    ```bash
    larasail database init [--user wave] [--db wave]
    ```

    Update the `DB_CONNECTION`, `DB_HOST`, `DB_PORT`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD` fields in the `.env` file.

5. **Migrate and Seed the Database**:

    ```bash
    php artisan migrate
    php artisan db:seed
    ```

6. **Set the `APP_URL`**:

    Update the `APP_URL` in the `.env` file with your domain or IP address:

    ```bash
    APP_URL=http://example.com
    ```

    It needs to exactly match the domain you used during the setup process including the protocol.

7. **Build Assets**:

    Build the static assets:

    ```bash
    npm install && npm run dev
    ```

---

## Step 6: Verify the Installation

1. Visit your Droplet's public IP address or domain in a web browser.
   If everything is configured correctly, you'll see the Wave installation screen.

2. Log in with the default admin credentials:
   - **Email**: `admin@admin.com`
   - **Password**: `password`

---

## Additional Notes

- **Managed Databases**: If using a DigitalOcean Managed Database, connect Wave by updating the `DATABASE_URL` in the `.env` file with the provided credentials.
- **SSL Configuration**: Run the following if SSL wasn't enabled initially:

    ```bash
    certbot --nginx -d example.com -d www.example.com
    ```

---

Wave is now ready to sail on DigitalOcean! Raise the anchor and prepare for smooth sailing ahead. For more customization options, check out [Wave's documentation](https://wave.devdojo.com/).
