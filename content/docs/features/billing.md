---
title: Billing
description: Implement Billing and Payments into your app
prevTitle: 'User Impersonations'
prevURL: '/docs/features/user-impersonations'
nextTitle: 'Subscription Plans'
nextURL: '/docs/features/subscription-plans'
---

# Billing

Wave integrates seamlessly with <a href="https://stripe.com" target="_blank" class="underline">Stripe</a> or <a href="https://paddle.com" target="_blank" class="underline">Paddle</a> in order to accept payments in your app. In this section you will learn how to configure and setup billing in your application.

- [Billing](#billing)
  - [Selecting Your Payment Provider](#selecting-your-payment-provider)
  - [Stripe](#stripe)
    - [Add Stripe API Credentials](#add-stripe-api-credentials)
    - [Add Stripe Webhook Secret](#add-stripe-webhook-secret)
    - [Webhook Warning](#webhook-warning)
    - [Testing Sripe Payments and Events](#testing-sripe-payments-and-events)
    - [Stripe Customer Portal](#stripe-customer-portal)
  - [Paddle](#paddle)
    - [Paddle Environment](#paddle-environment)
    - [Paddle API Credentials](#paddle-api-credentials)
    - [Paddle Webhooks](#paddle-webhooks)
    - [Paddle Payment link](#paddle-payment-link)
  - [Test Billing Process](#test-billing-process)

## Selecting Your Payment Provider

You may choose whichever payment provider fits your needs. To change the payment provider you want to use, you can change the `BILLING_PROVIDER` value inside your application `.env` file. You can set this to **stripe** or **paddle**. This config is stored inside the `config/wave.php` file.

```php
<?php

return [

	...
	'billing_provider' => env('BILLING_PROVIDER', 'stripe'),
	...

];
```

Ok, now that you've selected the payment provider, lets dig in a little deeper into each one to learn how to get it setup.

<a name="stripe"></a>
## Stripe

Wave utilizes <a href="https://docs.stripe.com/payments/checkout" target="_blank">Stripe Checkout</a>, which is the simplest implementation of accepting payments. In order to get setup you'll need the following credentials.

- Stripe Publishable Key
- Stripe Secret Key
- Stripe Webhook Secret

<a name="api-credentials"></a>
### Add Stripe API Credentials

To get the **Publishable Key** and **Secret Key**, follow these steps:

1. Log in to your Stripe account at <a href="https://dashboard.stripe.com" target="_blank">dashboard.stripe.com</a>.
2. Click on the **Developers** button at the top right corner of the dashboard.
3. From the dropdown menu, select **Api Keys**.
4. You will see your **Publishable key** and **Secret key**. Copy these values and place them in your application *.env* file:

```bash
STRIPE_PUBLISHABLE_KEY=pk_test_51...
STRIPE_SECRET_KEY=sk_test_51...
```

<a name="api-credentials"></a>
### Add Stripe Webhook Secret

The **Webhook Secret** key allows stripe to talk to your application and receive webhook events when a customer fullfills a purchase, changes their plan, or cancels a subscription. Follow these steps, to get this key:

1. Log in to your Stripe account at <a href="https://dashboard.stripe.com" target="_blank">dashboard.stripe.com</a>.
2. Click on the **Developers** button at the top right corner of the dashboard.
3. From the dropdown menu, select **Webhooks**.
4. From this page you will see a button to **Create new endpoint**
5. From this screen you will need to check all of the **Checkout Events** and all of the **Billing Portal Events**, then click continue.
6. Enter your application endpoint. This will be your application URL with the `/webhook/stripe` path. So, if your URL is `https://wave.test` your endpoint will be `https://wave.test/webhook/stripe`.
7. Optionally, add a description and click the **Create destination** button.
8. On this page you will see a **Signing secret** key inside the **Destination Details** section. Copy this value and add it to your application *.env* file:

```bash
STRIPE_WEBHOOK_SECRET=whsec_75...
```

### Webhook Warning

If your webhook is not setup correctly, it may look like the user purchases and their account never upgrades. Here is a workflow overview of how it works from when the user clicks the **Subscribe to Plan** button.

<img src="https://cdn.devdojo.com/images/august2024/stripe-webhook-workflow-new.png" class="relative w-full border rounded-md border-neutral-200" />

As you can see that the webhook gets sent at the same time as a successful payment. So, if the webhook is not setup correctly the user will be redirected to the success page, but their account will not actually be upgraded.

As long as the webhook is setup correctly, the functionality will happen simultaneously, so everything will function correctly. This is probably a good thing to know in case you are having trouble debugging the situation where an account never gets upgraded after a successful purchase.

We may change the way that this works down the road, but for now it's good to know about how this functions.

<a name="testing-stripe-payments-events"></a>
### Testing Sripe Payments and Events

It's very important to test your application from a dev environment to make sure everything is working correctly. At the top right of your stripe dashboard you can toggle **Test Mode** on and off. You will receive new API keys for each environment, so make sure to add the correct keys.

When you want to test out payments locally, you can use these <a href="https://docs.stripe.com/testing#cards" target="_blank">Example Credit Card Credentials</a> during checkout.

Next, if you want to easily test out events on your local machine you can <a href="https://docs.stripe.com/stripe-cli" target="_blank" target="_blank">utilize the Stripe CLI</a>, and <a href="https://docs.stripe.com/webhooks#test-webhook">test your webhook events locally</a>.

After setting up the Stripe CLI, you will run the following command:

```bash
stripe listen --forward-to https://wave.test/webhook/stripe
```

In this example, you need to swap out `https://wave.test` with your local URL. After running this command, you'll get a message that says something like **Your webhook signing secret is whsec_75...**, this is the new *STRIPE_WEBHOOK_SECRET* you will need to add to your `.env` file.

Now you will be able to go through your application check out process and see how everything will function when a user subscribes, switches plans, or cancels.

<a name="stripe-customer-portal"></a>
### Stripe Customer Portal

After a user subscribes to a plan they will then visit the **Stripe Customer Portal** to update plans, change their payment methods, or cancel their plan.

You can configure the Stripe customer portal by following these steps:

1. Log in to your Stripe account at <a href="https://dashboard.stripe.com" target="_blank">dashboard.stripe.com</a>.
2. Click on the **Settings** button at the top right.
3. From the settings page, click **Billings**.
4. From the billing page you will see a tab that says **Customer portal**

Here you can customize all the aspects of the customer portal.

<a name="paddle"></a>
## Paddle

Paddle also offers a very simple <a href="https://developer.paddle.com/concepts/sell/self-serve-checkout" target="_blank">Checkout integration</a>. This is the integration that we'll be using. In order to setup this implementation we'll need 4 different keys.

1. Paddle Vendor ID
2. Paddle API Key
3. Paddle Public Secret
4. Paddle Webhook Secret

### Paddle Environment

When you are implementing your Paddle integration you will want to test the payment process using <a href="https://sandbox-vendors.paddle.com/" target="_blank" class="font-bold">Sandbox Mode</a>. To do this, you need to specify the `PADDLE_ENV` value inside your `.env` file:

```
PADDLE_ENV=sandbox
```

When, you're ready to put your application in production you will change the `PADDLE_ENV` to `production`. Next, we need to add our API credentials.

### Paddle API Credentials

Inside of your Paddle Dashboard you'll see a button under the **Developer Tools** menu, called **Authentication**, click on that button to get your API Authentication Credentials.

<img src="https://cdn.devdojo.com/images/august2024/paddle-api-keys.png" class="w-full rounded-md" />

From this page, you can get your **Vendor ID (seller ID)**, **API Key**, and **Client-side Token**. To get the API Key and Public key, you'll need to **+ Generate** a new key if you do not have one. Then, click the *Show Key* button in the menu to the right. Paste the key values into your application `.env` file:

```
PADDLE_VENDOR_ID=9999
PADDLE_API_KEY=...
PADDLE_CLIENT_SIDE_TOKEN=...
```

Next, we need to setup our webhook.

### Paddle Webhooks

Paddle webhooks are used to send events to your application. These events include a user subscription being created, cancelled, updated, or a payment has failed. In order for your app to handle these events correctly we have to setup a webhook. To do this, go to your Paddle dashboard and click on **Developer Tools** -> **Notifications**.

<img src="https://cdn.devdojo.com/images/august2024/paddle-webhook.png" class="w-full" />

From the slide over menu, you will need to add your application URL and the path `webhook/paddle`. If you are in Sandbox mode, to test this out you may need to Publicly Share your local site and update that public URL inside the field.

You will also need to check all the events that we want to send to our application.

<img src="https://cdn.devdojo.com/images/august2024/paddle-events.png" class="w-full" />

Make sure to select the `subscription.cancelled`, `subscription.created`, `subscription.updated`, and `transaction.payment_failed`. Those are the events that we handle on Waves end.

Finally, we need to set our payment link.

### Paddle Payment link

Paddle needs to know your default payment link. This is users will be redirected when they cancel or make upates on Paddles end. To update this payment link, from the left menu under **Checkout**, click the **Checkout Settings** button and then scroll down to **Payment Links**.

The default payment link should be set to `http://yourdomain.com/settings/subscription`.

<img src="https://cdn.devdojo.com/images/august2024/payment-link.png" class="w-full" />

## Test Billing Process

You can test out the Stripe or Paddle implementation using the following credentials:

```
Credit Card: 4242 4242 4242 4242
Expiration: Any Future Date
CVC: Any three digit code
```

More information below about Test Credit Cards for each provider:

 - <a href="https://docs.stripe.com/testing#cards" target="_blank">Stipe Test Cards</a>
 - <a href="https://developer.paddle.com/concepts/payment-methods/credit-debit-card#test-payment-method" target="_blank">Paddle Test Cards</a>

Before we can fully test out your integration, you will need to add a few <a href="{ url('/docs/features/subscription-plans') }">Subscription Plans</a>. We'll cover that next.