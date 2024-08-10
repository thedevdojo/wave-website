---
title: User Roles and Permissions
description: Assign roles and Permissions to users in your application
prevTitle: 'Subscription Plans'
prevURL: '/docs/features/subscription-plans'
nextTitle: 'User Notifications'
nextURL: '/docs/features/notifications'
---

# Roles and Permissions

Roles and Permissions allow you to manage who can access different parts of your web application.


## Roles

Roles are labels or titles that you give to users in your web application to define what they can or cannot do. By default, Wave ships with five roles:

1. **Admin** - This is the role you will have as the developer and administrator.
2. **Registerd** - This is the default role for a newly registered user
3. **Basic** - This is a role associated with a Basic Subscriber Plan
4. **Premium** - This is a role associated with a Premium Subscriber Plan
5. **Pro** - This is a role associated with a Pro Subscriber plan

The **Admin** role should not be modified as there are many references to this role in the codebase; however, you may modify any of the other roles.

The **Registered** role is the default role that every user will have when they register for an account with your application. If y ou wish to change the name of this role, make sure that you also modify the `default_user_role` value inside of the `wave.php` config file.

Next, you may also modify/delete any of the **Basic**, **Premium**, and **Pro** roles to meet the needs of your application. These roles are associated with a **Subscription Plan**. You'll notice that Wave also ships with a **Basic**, **Premium**, and **Pro** plan. The mindset here is that when a user upgrades or purchases a plan, they will be assigned a role that corresponds to that plan. 

> For organizational purposes, if you change the **Basic** role to **Starter**, you may also want to update the name of the **Basic** plan to **Starter** as well.

It’s not mandatory for the user **Role** to have the same name as the **Plan**; however, doing so will make things easier to understand. Additionally, a user doesn’t have to have only one Role; but, keeping it this way will make things easier to comprehend and manage.


## Digging Deeper

Wave utilizes the popular <a href="https://github.com/spatie/laravel-permission" target="_blank" class="underline">Spatie Permissions Package</a> to handle the inner-workings of the **Roles** and **Permissions** functionality. You may refer to <a href="https://spatie.be/docs/laravel-permission" target="_blank" class="underline">this documentation</a> to learn how roles/permissions work in more depth.