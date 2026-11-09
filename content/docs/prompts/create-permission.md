---
title: Create a Permission
description: Create a permission and assign it to roles using an artisan command
prevTitle: 'Create a Role'
prevURL: '/docs/prompts/create-role'
nextTitle: 'Create a Plugin'
nextURL: '/docs/prompts/create-plugin'
---

## Create a Permission

The `app:create-permission` command creates a new permission and lets you assign it to one or more roles straight away.

### Command Signature

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```bash
php artisan app:create-permission
```
</div>

### Usage

When you run the command, it will prompt you for:

1. The name of the new permission, for example `edit articles`
2. Whether you want to assign the permission to roles
3. If yes, the roles that should get it. You can select several.

Every user with one of the selected roles gets the permission. You can check it with `auth()->user()->can('edit articles')` or the `@can('edit articles')` Blade directive.

### Validation Rules

The permission name is:

- Required
- A string of at most 255 characters
- Unique in the permissions table

If the name isn't valid, the command shows the errors and exits with status code 1.

### Success Output

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```shell
Permission assigned to: premium, pro
Permission 'edit articles' created successfully.
```
</div>

### Notes

- Selecting roles uses `syncRoles`, so the permission ends up on exactly the roles you picked.
- You can change which roles have a permission later in the admin: edit the permission under **Permissions**, or edit a role under **Roles** and tick its permissions.
- See [Roles and Permissions](/docs/features/roles-permissions) for checking permissions in your code.
