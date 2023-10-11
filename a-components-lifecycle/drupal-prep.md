# Drupal prep

Before we can dive into building our component's infrastructure in Drupal, we need to get a few things ready. Perform each of the tasks below:

## Exercise: Enable the new theme

Enabling our new theme is not required to build Drupal's back-end for the Hero, but it's something we need to do at some point. Let's do it now:

1. From Drupal's Admin Toolbar click **Appearance**
2. Scroll to the **Uninstalled themes** section where you will find the new theme you created. It should have a thumbnail image with the Mediacurrent logo
3. Click **Install and set as default** under the theme name

## Exercise: Disable CSS/JavaScript Aggregation

Drupal core comes with CSS and Javascript Aggregation turned on out of the box. Although this is highly recommended on production websites, during development it is recommended we turn aggregation off. This will ensure CSS and Javascript code we write will be instantly available on our drupal pages without having to continuously clean Drupal caches.

**Option 1: Development Services**

I recommend using the settings.local.php and development.services.yml files to disable caching programmatically. This way you don't accidentally leave cache or aggregation off in production.

Follow this setup: [<mark style="color:orange;">https://www.drupal.org/node/2598914</mark>](https://www.drupal.org/node/2598914)

```
# Local development services.
#
# To activate this feature, follow the instructions at the top of the
# 'example.settings.local.php' file, which sits next to this file.
parameters:
  http.response.debug_cacheability_headers: true
  twig.config:
    debug: true
    auto_reload: true
    cache: false
services:
  cache.backend.null:
    class: Drupal\Core\Cache\NullBackendFactory
```

**Option 2: Drupal UI**

* From Drupal's Admin toolbar click **Configuration > Development > Performance**
* Clear both check boxes: **Aggregate CSS files** & **Aggregate JavaScript files**
* Click the **Save configuration** button

While you're at it, click the **Clear all caches** button on the same page
