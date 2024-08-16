---
title: API
description: Learn how to use the API
prevTitle: 'Blog'
prevURL: '/docs/features/blog'
nextTitle: 'Admin'
nextURL: '/docs/features/admin'
---

# API

Wave comes with an out-of-the-box API, which will allow you to provide an API to your users or build a mobile app from your API.

In this section we will go into more depth on how you can use the Wave API.

- [API](#api)
    - [User API Keys](#user-api-keys)
  - [Access Tokens](#access-tokens)
    - [Get Access Token from API Key](#get-access-token-from-api-key)
    - [Get Access Token from Login](#get-access-token-from-login)
    - [Request Data From an Access Token](#request-data-from-an-access-token)
  - [Testing Your API](#testing-your-api)
  - [Registering via the API](#registering-via-the-api)
  - [JWT VS Sanctum](#jwt-vs-sanctum)

---

### User API Keys

Any user may create an API key by visiting the API settings page at: `/settings/api`, then to create a new API key, enter a name in the textbox and click on the `Create New Key` button.

<img src="https://cdn.devdojo.com/images/august2024/create-new-key.png" alt="Create New Key" class="w-full" />

After creating your new API key you will see it in the list of *Current API Keys*. You'll be able to see the Name and the Date Created. In this table you may also view, edit, or delete any key. Click the `View` button.

<img src="https://cdn.devdojo.com/images/august2024/view-button.png" alt="View Button" class="w-full" />

And you will see the current API key where you can copy and paste it to be used.

<img src="https://cdn.devdojo.com/images/august2024/copy-api-key.png" alt="Copy API Key" class="w-full" />

Next, when you click on the edit button, you will be able to edit the current API key name.

<img src="https://cdn.devdojo.com/images/august2024/edit-api-key.png" alt="Edit API Key" class="w-full" />

Lastly, if you click on the delete button:

<img src="https://cdn.devdojo.com/images/august2024/delete-button.png" alt="Delete Button" class="w-full" />

You will be able to delete the current API key.

<img src="https://cdn.devdojo.com/images/august2024/delete-confirm.png" alt="Delete Confirm" class="w-full" />

## Access Tokens

In order to get data from your API, you need an **Access Token**. You can get this access token in two ways:

1. User API key
2. User Email/password

When unencrypted, this access token will be associated with a user in your application. That is how you determine what kind of data is accessible.

### Get Access Token from API Key

To get an **Access Token** using an API Key, you can submit a POST request to:

```php
/api/token?key=API_KEY_HERE
```

And this will get a response that looks similar to the following:

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC93YXZlLnRlc3RcL2FwaVwvdG9rZW4iLCJpYXQiOjE1Mzk4MDg4OTUsImV4cCI6MTUzOTgxMjQ5NSwibmJmIjoxNTM5ODA4ODk1LCJqdGkiOiJRdTViYnhwdlBkNE9tT3ZZIiwic3ViIjoyLCJwcnYiOiI4N2UwYWYxZWY5ZmQxNTgxMmZkZWM5NzE1M2ExNGUwYjA0NzU0NmFhIn0.AJNTXTlnI74ZyPw2rqvEaI7P5YPaLnZNWcCBBmRX0W0"
}
```

This is the **Access Token** we will use to retrieve data from your application.

### Get Access Token from Login

To get an **Access Token** from a User Login you can do a POST request to:

```php
/api/login?email=admin@admin.com&password=password
```

And you will get a similar response to the response above:

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC93YXZlLnRlc3RcL2FwaVwvbG9naW4iLCJpYXQiOjE1Mzk4MTE0NjUsImV4cCI6MTUzOTgxNTA2NSwibmJmIjoxNTM5ODExNDY1LCJqdGkiOiJKRWljOGdTWFp4S0VjaWh1Iiwic3ViIjoxLCJwcnYiOiI4N2UwYWYxZWY5ZmQxNTgxMmZkZWM5NzE1M2ExNGUwYjA0NzU0NmFhIn0._1oFRK-zeUKMpvCcg8kmM86avzzmI--yQnI4KRwYk1k",
    "token_type": "bearer",
    "expires_in": 60
}
```

You'll see that this response includes 2 more fields the `token_type` and the `expires_in`. When your app detects the access token has expired it needs to request a new access token via the following request:

| METHOD | URI | Bearer TOKEN |
| ------ | --- | ____________ |
| POST | `/api/refresh` | Bearer: eyJ0e... |

And you will recieve a new **Access Token** for your application to be used. This expiration and refresh tokens are common for keeping your API secure.

### Request Data From an Access Token

You are responsible for the data you want your users to access via the API. You can simply check which user is making this API request and detect if they have the correct roles/permissions, or you can also try some of these popular API packages.

- <a href="https://filamentphp.com/plugins/rupadana-api-service" class="underline" target="_blank">Filament API Service</a>
- <a href="https://github.com/tailflow/laravel-orion" class="underline" target="_blank">Laravel Orion Rest API</a>
- <a href="https://restify.binarcode.com/" class="underline" target="_blank">Restify</a>
- <a href="https://laravelapitoolkit.com/" class="underline" target="_blank">Laravle API Toolkit</a>

The packages listed above offer a simple way to create a REST API from your current Laravel application. It is entirely up to you how you want to handle your REST API in your application.

## Testing Your API

You can test out your application by using a third-party tool called <a href="https://insomnia.rest/" target="_blank">Insomnia</a>, this is a free app that you can download and view all the response from your API endpoints.

<img src="https://cdn.devdojo.com/images/august2024/insomnia.png" class="w-full" alt="Insomnia Screenshot" />

In order to download the End Points for the Wave application you can find this file located here: [https://github.com/thedevdojo/laravel-wave-api-endpoints](https://github.com/thedevdojo/laravel-wave-api-endpoints). You will want to make sure that you use the **wave-3-api-endpoints.json**. You will also want to checkout the additional instructions in the **ReadmeV3.md**.

After you have imported the API endpoints, you may also wish to change the BASE_URL variable in the application. We use `https://wave.test` for testing, but your local URL may be different. To do this, click on the `base_url` icon at the beginning of any endpoint.

<img src="https://cdn.devdojo.com/images/august2024/click_base_url.png" class="w-full" alt="Base URL button" />

Then, you'll need to change the `base_url` value to your application URL.

<img src="https://cdn.devdojo.com/images/august2024/base_url_change.png" class="w-full" alt="Base URL change" />

And, now you're ready to test out your API.

## Registering via the API

If you are creating an API, you may also wish to allow your users to register. This is simple as well. You can perform a POST request to:

```php
/api/register?name=John Doe&username=jdoe&email=jdoe@gmail.com&password=pass
```

And a new user will be registered and given an Access Token to access data via your API.


## JWT VS Sanctum

The current API that Wave ships with is a stateless JWT API. This means that when a request is made to the API, it does not store a state for the current user. Each request is validated. Sanctum allows API access via a simple access token and does not have functionality for logging a user in or registering. When a user authentocates via Sanctum the server stores an authenticated user in the sessions (which makes it a stateful authentication).

We may wish to include Sanctum in your project and it will work alongside the current JWT implementation.