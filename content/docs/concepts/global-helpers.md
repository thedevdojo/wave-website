---
title: Global Helpers
description: Wave offers some global helper functions that you may use anywhere in your application
prevTitle: 'Blade Directives'
prevURL: '/docs/concepts/blade-directives'
nextTitle: 'Volt Pages'
nextURL: '/docs/concepts/volt'
---

# Global Helpers

Wave also has a few global helpers for you to use in your application.

### setting()

In the admin section of your application you'll see a settings button at the bottom of the menu. This will take you to the admin settings page at  `/admin/settings`. Screenshot below.

<img src="https://cdn.devdojo.com/images/october2024/admin-settings-page.png" class="rounded-md" />

From here, you can add any type of key/value setting and then use it in your application, like so:

```php
echo setting('site.title');
```

You'll see that these settings are being used as a fallback SEO title and description if one is not set, inside of `resources/themes/theme_name/partials/head.blade.php`:

```php
@if(isset($seo->title))
    <title>{{ $seo->title }}</title>
@else
    <title>{{ setting('site.title', 'Laravel Wave') . ' - ' . setting('site.description', 'The Software as a Service Starter Kit built with Laravel') }}</title>
@endif
```

You'll also see that inside of the `resources/views/themes/theme_name/partials/footer_scripts.blade.php`, we are using the a setting to display google anayltics if the key has been entered:

```php
@if(setting('site.google_analytics_tracking_id', ''))
    <!-- Global site tag (gtag.js) - Google Analytics -->
    <script async src="https://www.googletagmanager.com/gtag/js?id={{ setting('site.google_analytics_tracking_id') }}"></script>
    <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());

        gtag('config', '{{ setting("site.google_analytics_tracking_id") }}');
    </script>
@endif
```

So, if you update the `site.google_analytics_tracking_id` with your Google analytics id, then analytics will automatically start tracking on your website.

---

You can use these **key/value** settings however you see fit in your theme. If you start using them often, it might be helpful to prefix them in a group, you'll see that all of the current settings are prefixed with `site.` because all these settings are specific to the site itself.

### blade()

We've also created a `blade()` helper that will take any blade code and convert it to HTML, as an example:

```php
@php $name = 'Tony'; @endphp
<p>Hello, my name is {{ $tony }}</p>
```

Passing a string like this above to the `blade()` method, will output the following:

```html
<p>Hello, my name is Tony</p>
```

### getMorphAlias($class)

This global method will take in any class and return the Morph alias for that specific class. Example, passing it `\App\Models\User::class`, will return `user`.

### has_monthly_yearly_toggle()

This method will return true or false if the pricing template should show the monthly/yearly toggle. Sometimes a user may only have monthly pricing plans or only yearly pricing plans. In that case we don't want to show the toggle switch.

### get_default_billing_cycle()

This will return the default billing cycle, by default it will return `Monthly`, but if the user only has **yearly** plans, it will return `Yearly`. This will help you determine which pricing plans to show by default.

---

As we add more global helper methods to Wave, we'll be sure to document them here as well. If you have an idea for some global helper methods, you would like to see, please <a href="https://github.com/thedevdojo/wave/compare" target="_blank">submit a PR</a>.


