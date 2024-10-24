---
title: Authentication
description: Learn how the authentication works with-in Wave
prevTitle: 'Upgrading'
prevURL: '/docs/upgrading'
nextTitle: 'User Profiles'
nextURL: '/docs/features/user-profiles'
---

# Authentication

Wave is built on top of <a href="https://devdojo.com/auth" target="_blank">DevDojo Auth</a>, which means your application will have all the authentication features you need for most use-cases. Be sure to refer to the <a href="https://devdojo.com/auth" target="_blank">Auth docs</a> for more advanced configurations.

- [Authentication](#authentication)
- [Auth Customizations](#auth-customizations)
- [Available Authentication Pages](#available-authentication-pages)
    - [Login](#login)
    - [Registration](#registration)
    - [Verify Email](#verify-email)
    - [Password Confirmation](#password-confirmation)
    - [Password Reset/Request](#password-resetrequest)
    - [Two-Factor Challenge](#two-factor-challenge)
  - [Social Authentication](#social-authentication)

# Auth Customizations

Our Auth package includes a setup route that will allow you to upload a logo, change your color scheme and more. If you visit `/auth/setup` you'll see a setup page in front of you that will provide a handful of customization options.

<img src="https://cdn.devdojo.com/images/august2024/devdojo-auth-setup.jpeg" class="w-full h-auto rounded-md" />

# Available Authentication Pages

Below is a quick list of all the authentication pages you get out of the box:

- Login
- Register
- Verify Email
- Password Confirmation
- Password Reset Request
- Password Reset
- Two-Factor Challenge

Let's dig into each page a little deeper.

### Login

After a user has created an account through your application, they can login by visiting the `/auth/login` route. After successfully logging in the user will then be redirected to their dashboard.

> With a fresh installation of Wave your app will have a default admin account. To use this account you can login with the following email `admin@admin.com` and password as `password`

### Registration

By default, all users can register for a free account; however, if you wanted users to be a subscriber before accessng your app, you can add the `subscribed` middleware to the dashboard and many other pages. This will restrict access to a specific page unless a user is a subscriber.

> You can use the `subscribed` middleware in place of the `auth` middleware, no need to include them both. The `subscribed` middleware will also check that the user is logged in and if not it will redirect them to the login page.

Otherwise, you may offer your users a Free minified version of your SaaS and encourage them to upgrade to a subscription plan with more advanced and bonus features.

If you wish to add some additional functionality when a user registers, you may add this to your `App\Models\User` model inside of the `boot()` method. As you can see we've already added some functionality to dynamically create a username from an email and assign the user with the default user role upon registration.

<include src="docs/filename-top.html"></include><include src="docs/filename.html" file="App/Models/User.php"></include>

```php
protected static function boot()
{
    parent::boot();
    
    // Listen for the creating event of the model
    static::creating(function ($user) {
        // Check if the username attribute is empty
        if (empty($user->username)) {
            // Use the name to generate a slugified username
            $username = Str::slug($user->name, '');
            $i = 1;
            while (self::where('username', $username)->exists()) {
                $username = Str::slug($user->name, '') . $i;
                $i++;
            }
            $user->username = $username;
        }
    });

    // Listen for the created event of the model
    static::created(function ($user) {
        // Remove all roles
        $user->syncRoles([]);
        // Assign the default role
        $user->assignRole( config('wave.default_user_role', 'registered') );
    });
}
```
</div>

You may modify this functionality as needed or add more functionality to it.

### Verify Email

In order to turn on Email Verification and require your users to verify their email before accessing your application, you can toggle that setting from the Auth Settings page (`/auth/setup/settings`), toggle on the **Registration Require Email Verification**, and users will now be required to verify email before accessing your application.

<img src="https://cdn.devdojo.com/images/august2024/require-email-verification.png" class="w-full h-auto rounded-md" />

Please refer to <a href="https://devdojo.com/auth/docs/config/email/" target="_blank">this documentation</a> to learn how to modify the logo in your emails.


### Password Confirmation

There may be parts of your application where you want users to confirm their password before being able to access your application. You can add the middleware name `confirm` to any page/route and the user will be required to re-enter their password.

### Password Reset/Request

The password Request page allows users to enter in their email address. They will then be sent a unique password link in their email. Upon visiting that link they will be prompted to reset their password.

### Two-Factor Challenge

You can also give your users the option of enabling Two-Factor auth to gaurantee security in their account. Learn more about <a href="https://devdojo.com/auth/docs/config/two-factor-auth/" target="_blank">setting up 2FA and enabling it for your users here</a>.

## Social Authentication

Setting up Social Authentication is very simple thanks to the Auth Package. From inside the `/auth/setup/providers` you can toggle the social networks you want to enable.

<img src="https://cdn.devdojo.com/images/august2024/social-providers-screen.jpeg" class="w-full border rounded-md border-neutral-200" />

You will also need to add the social network API keys in order to successfully enable the provider. <a href="https://devdojo.com/auth/docs/config/social-providers/" target="_blank">Learn more about that here</a>.