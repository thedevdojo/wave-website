---
title: Billing
description: Implement Billing and Payments into your app
nextTitle: 'Live-Reloading'
nextURL: '/docs/features/live-reloading'
prevTitle: 'Collections'
prevURL: '/docs/features/collections'
---

# Billing

Wave integrates seamlessly with <a href="https://stripe.com" target="_blank" class="underline">Stripe</a> or <a href="https://paddle.com" target="_blank" class="underline">Paddle</a> in order to accept payments in your app. In this section you will learn how to configure and setup billing in your application.

- [Billing](#billing)
  - [Stripe](#stripe)
    - [Add Stripe API Credentials](#add-stripe-api-credentials)
    - [Add Stripe Webhook Secret](#add-stripe-webhook-secret)
    - [Testing Sripe Payments and Events](#testing-sripe-payments-and-events)
    - [Stripe Customer Portal](#stripe-customer-portal)
  - [Paddle](#paddle)
    - [Add Paddle API Credentials](#add-paddle-api-credentials)
  - [Default payment link](#default-payment-link)
  - [Webhooks](#webhooks)
      - [Ready to go Live?](#ready-to-go-live)
    - [Test Billing Process](#test-billing-process)

<a name="stripe"></a>
## Stripe

Stripe is an online payment platform that enables your application to receive payments from customers. Wave utilizes <a href="https://docs.stripe.com/payments/checkout" target="_blank">Stripe Checkout</a>, which is the simplest implementation of accepting payments. In order to get setup you'll need the following credentials.

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

<a name="paddle-api-credentials"></a>
### Add Paddle API Credentials

Inside of your Paddle Dashboard you'll see a button under the **Developer Tools** menu, called **Authentication**, click on that button to get your API Authentication Credentials.

![paddle-authentication.png](https://imgur.com/xdDuVKn.png)

Along with the **API Auth Code**, you'll also need to get your **Client Side Token**.

On this page you'll find your **Seller ID** and your **API Auth Code**. These are the credentials that you will need to add to your `.env` file for `PADDLE_VENDOR_ID`, `PADDLE_API_KEY` and `PADDLE_CLIENT_SIDE_TOKEN`:

```
PADDLE_VENDOR_ID=9999
PADDLE_API_KEY=YOUR_REALLY_API_KEY_HERE
PADDLE_CLIENT_SIDE_TOKEN=YOUR_CLIENT_SIDE_TOKEN
PADDLE_ENV=sandbox
```

After adding these credentials, your application has been successfully configured with Paddle.

## Default payment link

Wave uses the default Paddle payment link to handle the payment process. You have to set up the default payment link in your Paddle account. To do this, go to your Paddle dashboard and click on **Checkout Settings** scroll down to **Payment Links**.

The default payment link should be set to `http://yourdomain.com/settings/subscription`.

![](https://imgur.com/zboWobt.png)

## Webhooks

Wave uses Paddle webhooks to handle the payment process. You have to set up the webhooks in your Paddle account. To do this, go to your Paddle dashboard and click on **Developer Tools** -> **Notifications**.

![](https://imgur.com/QqJTggu.png)

Make sure to select the `subscription.cancelled` event so that Wave can handle the subscription cancellation process in case a user cancels their subscription or their payment fails.

> **Note**: Wave currently only supports the `subscription.cancelled` event. More events will be supported in the future.

#### Ready to go Live?

When you are ready to go live and take live payments you'll want to change the `PADDLE_ENV` from `sandbox` to `live`, and you'll be ready to accept live payments 💵

<a name="test-billing"></a>
### Test Billing Process

Before you can test out the full billing process, you will need to add a few [Subscription Plans](/docs/features/subscription-plans).

**Notice**: If you are using a Sandbox account, you will need to test your app from a `http://localhost` URL. The best way to do this is to utilize the laravel **Artisan Serve** command, or you can use [Laravel Sail](https://www.youtube.com/watch?v=WGhiY5xamms) docker image to serve up your app from a localhost URL.

After adding subscription plans and configuring your application with your Paddle API keys, you will now be able to test out the billing process using the following credentials:

```
Credit Card: 4242 4242 4242 4242
Expiration: Any Future Date
CVC: Any 3 digit code
```

---

After adding your Paddle API credentials, you'll need to configure your app with a few [Subscription Plans](/docs/features/subscription-plans) in order to test out the whole process. Let's move on to the [next step](/docs/features/subscription-plans) where you will learn how to do this.