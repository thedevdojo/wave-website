---
title: User Notifications
description: Learn how to add content to your website
prevTitle: 'Roles & Permissions'
prevURL: '/docs/features/roles-permissions'
nextTitle: 'Changelog'
nextURL: '/docs/features/changelog'
---

# User Notifications

Wave leverages the default <a href="https://laravel.com/docs/notifications" target="_blank">Laravel Notification</a> system and gives you an elegant UI to display those notifications in your app.

- [User Notifications](#user-notifications)
  - [When to use Notifications](#when-to-use-notifications)
  - [Creating Notifications](#creating-notifications)
  - [Viewing Notifications](#viewing-notifications)
  - [Getting the Notification Count](#getting-the-notification-count)
  - [Digging Deeper](#digging-deeper)

---

<a name="when-to-use"></a>
## When to use Notifications

When to use notifications in your application will be up to you. Here are a few examples:

1. Notify users in a forum discussion when a new response is added.
2. Notify a user when someone follows them.
3. Notify the user when someone sends them a message.

You get the general idea right? You are the creator and you can decide what kind of notifications your user will receive.

<a name="create-notifications"></a>
## Creating Notifications

We have built the Wave notifications on top of the default Laravel notifications, which are very simple to use and easy to implement.

> If you haven't checked out the Laravel notifications documentation, head on over to the official documentation at <a href="https://laravel.com/docs/notifications" target="_blank">laravel.com/docs/notifications</a>

To create a new notification, you can run the following artisan command:

```php
php artisan make:notification TestNotification
```

This will create a new file located at: `/app/Notifications/TestNotification`. This TestNotification should already be created inside every new Wave application. Here's the breakdown of what we've changed.

The via() method has been changed from:

```php
public function via($notifiable)
{
    return ['mail'];
}
```

to:

```php
public function via($notifiable)
{
    return ['database'];
}
```

And we've also modified this `toArray()` method:

```php
public function toArray($notifiable)
{
    return [
        //
    ];
}
```

to be:

```php
public function toArray($notifiable)
{
     return [
        'icon' => '/storage/users/default.png',
        'body' => 'This is an example, when the user clicks this notification it will go to the link.',
        'link' => '/dashboard',
         'user' => [
             'name' => 'John Doe'
         ]
    ];
}
```

You will want to update these methods when you create your own custom Notification. You can change any of hte attributes in the array, you will just need to update the variables that are referenced in the `pages/notifications/index.blade.php` view file.

--

Now, let's create a few notifications. We can do this by using the `tinker` command:

```php
php artisan tinker
```

Inside of the tinker command you will want to run the following command a few times:

```php
App\Models\User::find(1)->notify(new App\Notifications\TestNotification);
```

Swap out the `find(1)` with the **ID** of any user. After you have run that command, let's move on to learning how the user can view those notifications.

## Viewing Notifications

When a user is logged in, they will be able to visit the `/notifications` route and they will see a list of notifications.

<img src="https://cdn.devdojo.com/images/august2024/notifications.png" class="w-full" />

If a user does not have any notifications they will see a simple empty state message:

<img src="https://cdn.devdojo.com/images/august2024/notifications-empty.png" class="w-full" />

You can customize all of these views from inside your theme pages folder.


## Getting the Notification Count

To get the current notification count for any user, you can use the following code:

```php
auth()->user()->unreadNotifications->count()
```

## Digging Deeper

Be sure to check out <a href="https://laravel.com/docs/notifications" target="_blank">the Laravel Notifications documentation</a> to learn more.

