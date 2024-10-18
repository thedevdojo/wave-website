---
title: Create a Role
description: Learn how you can host your website and make it live for the world to see.
prevTitle: 'Create a User'
prevURL: '/docs/prompts/create-user' 
nextTitle: 'Create a Plugin'
nextURL: '/docs/prompts/create-plugin'
---

## Create a Role

The `app:create-role` command allows you to create a new role with optional permissions through an interactive command-line interface. This command is part of the Prompts section and utilizes Laravel's built-in prompt methods to gather role information and assign permissions.

### Command Signature

```
php artisan app:create-role
```

### Usage

When you run the command, it will prompt you for the following information:

1. Name of the new role
2. Description of the role (optional)
3. Whether you want to assign permissions to the role
4. If yes to permissions, selection of permissions to assign

### Step-by-step Process

1. Run the command in your terminal:

   ```
   php artisan app:create-role
   ```

2. Enter the requested information when prompted:
   - Role name
   - Role description (optional, press Enter to skip)

3. If any validation errors occur for the role name, the command will display them and exit. You'll need to run the command again with valid input.

4. After successful role creation, you'll be asked if you want to assign permissions to the role.

5. If you choose to assign permissions:
   - You'll be presented with a list of all available permissions in the database.
   - You can select multiple permissions using their corresponding numbers.

6. The command will assign the selected permissions to the role and display a success message.

### Validation Rules

The command applies the following validation rules for the role name:

- Required
- String
- Maximum 255 characters
- Must be unique in the roles table

### Permission Assignment

If you choose to assign permissions:

- The command fetches all available permissions from the database.
- You can select multiple permissions from the list provided.
- The selected permissions are synced to the role, removing any previously assigned permissions not in the new selection.

### Success Output

Upon successful role creation, the command will output a message like this:

```
Role '[Role Name]' created successfully.
```

If permissions are assigned, an additional message will be displayed:

```
Permissions assigned successfully.
```

### Error Handling

- If validation fails for the role name, the command will display all validation errors and exit with a status code of 1. You'll need to run the command again with correct input.
- If no permissions are found in the database when attempting to assign permissions, a warning message will be displayed.

### Notes

- This command uses the Spatie Permission package for role and permission management. Ensure that this package is properly installed and configured in your Laravel application.
- The command allows for an optional description of the role, which can be useful for providing context or details about the role's purpose.
- The permission assignment process uses the `syncPermissions` method, which means it will remove any existing permissions not included in the new selection.
- If you choose not to assign permissions during role creation, you can always assign them later using other methods provided by the Spatie Permission package.

Remember to use this command responsibly, especially in production environments, as it creates roles that can significantly affect your application's authorization structure.