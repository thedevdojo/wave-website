---
title: Blade Directives
description: Wave includes many helpful directives for you to use.
prevTitle: 'Plugins'
prevURL: '/docs/features/plugins'
nextTitle: 'Global Helpers'
nextURL: '/docs/concepts/global-helpers'
---

# Blade Directives

Wave includes a handful of directives to make building your application easier.

- [Blade Directives](#blade-directives)
    - [Auth and Guest](#auth-and-guest)
    - [Admin](#admin)
    - [Subscriber](#subscriber)
    - [Not Subscriber](#not-subscriber)
    - [Subscribed (to a specific plan)](#subscribed-to-a-specific-plan)
    - [Home](#home)
  - [Using the **@else** condition](#using-the-else-condition)

### Auth and Guest

This is not new to Wave; however, we want to document the auth directives for anyone who may not be familiar. The **@auth** directive checks if the user is authenticated, meaning they are logged in.

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
@auth
    <p>Welcome back, {{ auth()->user()->name }}!</p>
@endauth
```
</div>

In this example, the content inside the @auth directive is displayed only if the user is logged in. Inversely, the **@guest** directive checks if the user is not authenticated, meaning they are a guest (not logged in).

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
@guest
    <p>Please log in to continue.</p>
@endguest
```
</div>

In this case, the message is shown only if the user is not logged in.

### Admin

You can easily check if the user is logged in and they are an admin with the **@admin** directive.

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
@admin
    <p>You are logged in as an admin</p>
@endadmin
```
</div>

### Subscriber

You can easily check if the authenticated user is a subscriber with the **@subscriber** directive.

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
@subscriber
    <p>Thanks for subscribing to a plan and supporting us.</p>
@endsubscriber
```
</div>

### Not Subscriber

You may instead want to check if the user is not a subscriber using the **@notsubscriber** directive.

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
@notsubscriber
    <p>Upgrade to a plan?</p>
@endnotsubscriber
```
</div>

### Subscribed (to a specific plan)

If you wanted to check if a user is subscribed to a specific plan, you can reach for the **@subscribed($plan)** directive.

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
@subscribed('Basic')
    <p>You have subscribed to the Pro plan</p>
@endsubscribed
```
</div>

> You will need to specify the full name of the plan

### Home

We even have a simple route to check if the user is on the homepage, you can use the **@home** directive.

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```
@home
    <p>This is the home page ('/') route.</p>
@endhome
```
</div>

## Using the **@else** condition

With all these directives you can combine any of them with **@else**, for instance if you wanted to check if a user is a subscriber and you want to check the else condition, you can combine it like so:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```php
@subscriber
    <p>You are a subscriber</p>
@else
    <button>Become a subscriber</button>
@endsubscriber
```
</div>

The **@else** directive can be used with any of the conditions above.
