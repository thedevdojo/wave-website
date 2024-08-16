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

- [Roles and Permissions](#roles-and-permissions)
  - [Roles](#roles)
    - [Creating Roles](#creating-roles)
    - [Assigning Roles](#assigning-roles)
    - [Getting users with role](#getting-users-with-role)
    - [Checking if a user has role](#checking-if-a-user-has-role)
  - [Permissions](#permissions)
    - [Creating Permissions](#creating-permissions)
    - [Revoking Permissions](#revoking-permissions)
    - [Checking Permissions](#checking-permissions)
  - [Digging Deeper](#digging-deeper)

---

## Roles

Roles are labels that you give to users to define what they can or cannot do. By default, Wave ships with five roles:

1. **Admin** - This is the role you will have as the developer and administrator.
2. **Registerd** - This is the default role for a newly registered user
3. **Basic** - This is a role associated with a Basic Subscriber Plan
4. **Premium** - This is a role associated with a Premium Subscriber Plan
5. **Pro** - This is a role associated with a Pro Subscriber plan

The **Admin** role should not be modified as there are many references to this role in the codebase; however, you may modify any of the other roles.

The **Registered** role is the default role that every user will have when they register for an account with your application. If you wish to change the name of this role, make sure that you also modify the `default_user_role` value inside of the `wave.php` config file.

Next, you may also modify/delete any of the **Basic**, **Premium**, and **Pro** roles to meet the needs of your application. These roles are associated with a **Subscription Plan**. You'll notice that Wave also ships with a **Basic**, **Premium**, and **Pro** plan. The mindset here is that when a user upgrades or purchases a plan, they will be assigned a role that corresponds to that plan. 

> For organizational purposes, if you change the **Basic** role to **Starter**, you may also want to update the name of the **Basic** plan to **Starter** as well.

It’s not mandatory for the user **Role** to have the same name as the **Plan**; however, doing so will make things easier to understand. Additionally, a user doesn’t have to have only one Role; but, keeping it this way will make things easier to comprehend and manage.

### Creating Roles

You can easily create a role inside of your application from adding it in the admin. Alternatively, you may also create the new permission via code, like so:

```php
use Spatie\Permission\Models\Role;

$role = Role::create(['name' => 'writer']);
```

This will create a new role named **writer**. 

### Assigning Roles

You can then assign this role to any user, like so:

```php
auth()->user()->syncRoles([]);
auth()->user()->assignRole('writer');
```

Above, we are making sure that we remove all roles `syncRoles([])` and then assign the role of **writer**. You may decide to allow users to have multiple roles, which in that case you don't need syncRoles.

### Getting users with role

If you want to retrieve a list of all the users who have the **writer** role, you could do so like the following:

```php
$users = User::role('writer')->get();
```

This will return a collection of all users with the **writer** role.

### Checking if a user has role

If you want to check that a user has a specific role, you can do so like the following:

```php
auth()->user()->hasRole('writer');
```

Or directly from a blade view you can use this blade directive

```php
@role('writer')
    I am a writer!
@else
    I am not a writer...
@endrole
```

Next, if we wanted to be more granular with which users have access to specific features, we could use permissions.

## Permissions

You can create permissions and assign them to users or you can assign them to roles. This will make it easier when you want to create more granular permissions. Let's learn more about how we can use permissions.

### Creating Permissions

You can create a permission from the Admin panel, or you may also wish to do this in code:

```php
use Spatie\Permission\Models\Permission;

$permission = Permission::create(['name' => 'edit articles']);
```

Then, you can assign assign a permission to any role:

```php
use Spatie\Permission\Models\Role;

$role = Role::where('name', 'writer')->first();
```

You may also assign a permission specifically to a user:

```php
auth()->user()->givePermissionTo('edit articles');
```

These are referred to as direct permissions. Make sure that you are careful with adding permissions to roles and specifically to users. It can get a little complex if you don't keep it organized. It might be best to only assign permissions to roles. 

### Revoking Permissions

The reason that it's better to only assign permissions to roles is that you can easily revoke a permission from a role, like so:

```php
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

$role = Role::where('name', 'writer')->first();
$permission = Permission::were('name', 'edit articles')->first();

$role->revokePermissionTo($permission);
```

This means that all users of that role will all have that permission removed. You may also revokePermissions from a user.

### Checking Permissions

When you want to check if a user has a permission, you can do so like the following:

```php
auth()->user()->hasPermissionTo('edit articles');
```

This will check if the user has permission to **edit articles** either through their role or a direct permission. If you wanted to check for a few permissions, you can do something like this:

```php
auth()->user()->hasAnyPermission(['edit articles', 'publish articles', 'unpublish articles']);
```

If you are using blade files, you can use the following blade directives:

```php
@can('edit articles')
  //
@endcan
```

or use the `can()` method from the user object like this:

```php
@if(auth()->user()->can('edit articles') && $some_other_condition)
  //
@endif
```

## Digging Deeper

Make sure to checkout the <a href="https://github.com/spatie/laravel-permission" target="_blank" class="underline">Spatie Permissions Package</a> to learn more about **Roles** and **Permissions** functionality. This is the package that Wave uses under the hood to handle Roles/Permissions.