---
title: Create a User
description: Learn how you can host your website and make it live for the world to see.
prevTitle: 'Volt Pages'
prevURL: '/docs/concepts/volt' 
nextTitle: 'Create a Role'
nextURL: '/docs/prompts/create-role' 
---

## Create a User

The `app:create-user` command allows you to create a new user with role assignment through an interactive command-line interface. This command is part of the Prompts section and utilizes Laravel's built-in prompt methods to gather user information.

### Command Signature

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```bash
php artisan app:create-user
```
</div>

### Usage

When you run the command, it will prompt you for the following information:

1. User's name
2. User's email
3. User's username
4. User's password (input will be hidden)

After providing this information, the command will validate the input. If validation passes, it will create the user and then prompt you to select a role for the new user.

### Step-by-step Process

1. Run the command in your terminal:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```bash
php artisan app:create-user
```
</div>

2. Enter the requested information when prompted:
   - Name
   - Email
   - Username
   - Password (input will be hidden)

3. If any validation errors occur, the command will display them and exit. You'll need to run the command again with valid input.

4. After successful user creation, you'll be presented with a list of available roles. Select a role for the new user.

5. The command will assign the selected role to the user and display a success message.

### Validation Rules

The command applies the following validation rules:

- Name: Required, string, maximum 255 characters
- Email: Required, valid email format, maximum 255 characters, must be unique in the users table
- Username: Required, string, maximum 255 characters, must be unique in the users table
- Password: Required, must meet the default password requirements set in your Laravel application

### Role Assignment

The command fetches all available roles from the database and allows you to choose one for the new user. The user is assigned only the selected role, removing any previously assigned roles.

### Success Output

Upon successful user creation and role assignment, the command will output a message like this:

<include src="docs/filename-top.html"></include><include src="docs/file-buttons.html" file="none"></include>

```shell
User created successfully with role: [Selected Role Name]
```
</div>

### Error Handling

If validation fails, the command will display all validation errors and exit with a status code of 1. You'll need to run the command again with correct input.

### Notes

- The user is automatically marked as verified (`verified` column set to 1).
- This command uses the Spatie Permission package for role management. Ensure that this package is properly installed and configured in your Laravel application.
- The command syncs roles, meaning it will remove any existing roles before assigning the new one.

Remember to use this command responsibly, especially in production environments, as it creates fully verified users with assigned roles.