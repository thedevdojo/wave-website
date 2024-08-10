---
title: User Impersonations
description: Learn how the use user impersonations
prevTitle: 'User Profiles'
prevURL: '/docs/features/user-profiles'
nextTitle: 'Billing'
nextURL: '/docs/features/billing'
---

# User Impersonations

With user impersonations you can easily impersonate any user on your site. This will come in handy when you need to debug an issue that a specific user is experiencing.

Impersonating a user will allow you to login to your application acting as a specific user.

- [User Impersonations](#user-impersonations)
  - [Impersonate a User](#impersonate-a-user)

<a name="impersonate"></a>
## Impersonate a User

To impersonate a user you can visit your users section inside your admin at `/admin/users`. Find the user you want to impersonate and click on the Impersonate button.

<img src="https://cdn.devdojo.com/images/august2024/impersonate.png" class="w-full" />

You will now see that you are logged in as that specific user. You can open the user menu and you'll see a new **Leave Impersonation** button to exit that user account and log back in as your original admin user.

<img src="https://cdn.devdojo.com/images/august2024/impersonate-leave.png" class="w-full" />

We are utilizing a popular <a href="https://github.com/404labfr/laravel-impersonate" target="_blank">Impersonation Package</a> under the hood. Be sure to check out this package readme to learn more or extend the impersonation functionality.