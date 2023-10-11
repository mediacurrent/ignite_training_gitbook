# Drupal Libraries

In a Drupal 10 theme, stylesheets (CSS) and JavaScript (JS) are loaded through the same system for modules and themes, for everything: [asset libraries](https://www.drupal.org/node/2274843).

Drupal uses a high-level principle: assets (CSS or JS) are only loaded if you tell Drupal it should load them. Drupal does not load all assets on every page because it slows down front-end performance.

In the context of component-based theming, we are going to create a library for each individual component we build in Storybook. Each library will have all the CSS and JavaScript (if any), the component needs to render as expected.

{% hint style="danger" %}
**NOTE: Drupal libraries are only intended to work in Drupal**. The method attach\_library is ignored inside of Storybook. In Storybook we use Webpack to generate the CSS and JavaScript for components.
{% endhint %}

### Structure of a library

In your editor, open `training_theme.libraries.yml` (located in your theme's root). You will notice the global library already declared which includes all of the global theme styles that apply to all pages on the site (i.e. typography, brand colors, global styles, etc.). The global library looks something like this:

{% tabs %}
{% tab title="training_theme.libraries.yml" %}
```yaml
global:
  css:
    # The SMACSS category, "base", is loaded before other categories. Drupal 8/9
    # loads stylesheets based on the SMACSS ordering of:
    # base, layout, component, state, theme
    base:
      dist/css/bootstrap.css: {}
  dependencies:
    - "training_theme/icons"
    - "training_theme/fonts"
```
{% endtab %}
{% endtabs %}

1. **global:** This is the library name. When we build component's individual libraries, the library name will always be the name of the component it is for.
2. **css**: This is the asset we want to include in the library. Usually `css` and/or `js`.
3. **base**: The ordering category, in this case `base`, is loaded before other categories. Drupal 10 loads stylesheets based on the [SMACSS](https://smacss.com) ordering: `base`, `layout`, `component`, `state`, and `theme`. All of the components we create will use the `component` ordering. Drupal also groups/aggregates together assets that belong to the same category for performance reasons.
4. **dist/css/bootstrap.css: { }**: This is the path to the asset relative to the root of the theme. All assets in our theme are compiled into `dist/css` or `dist/js`. A library can have both of these assets. The path can also include multiple lines of assets. Say you are building a library for a component that uses a third party stylesheet, in addition to the path above you could include a new line with the path for the third party stylesheet. Same goes for JS assets.
5. **dependencies**: Here we can declare any global dependencies we want to load on every page. In this case we want to make custom icons and fonts loaded globally.

{% hint style="info" %}
Drupal Asset Libraries are powerful and there is so much more about them. Learn more about [Drupal Libraries](https://www.drupal.org/docs/8/creating-custom-modules/adding-stylesheets-css-and-javascript-js-to-a-drupal-8-module).
{% endhint %}

### Analyzing the 50/50 component

Let's see how our 50/50 component is rendered in Drupal.

* In the root of your Drupal theme, open `training_theme.libraries.yml` in your editor (replace `training_theme` if you used a different name for your theme).
* Somewhere in the file you will find the following definition for our 50/50 teaser:

{% tabs %}
{% tab title="training_theme.libraries.yml" %}
```yaml
teaser:
  css:
    component:
      dist/css/teaser.css: {}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**TIP**: Note the indentation in YML files which is essential to load library assets correctly.
{% endhint %}

Libraries are great because Drupal only loads what we need when we need it to avoid having to load assets that our page or component may never use. This helps with the site's performance.

### Attaching a library

But when is this library called in Drupal? There are many ways to load a library, but one of the most common ways to do this is through the attach\_library method. Let's revisit out teaser.twig template to see how this is done.

1. In your editor, open `src/patterns/components/teaser/teaser.twig`
2. Review the top of the file. Sure enough there is our call to the teaser library:

{% tabs %}
{% tab title="teaser.twig" %}
```php
{{ attach_library('training_theme/teaser') }}
```
{% endtab %}
{% endtabs %}

The `attach_library` function takes a path parameter which we are declaring by using the theme's namespace (the namespace is registered by the [Components Libraries](https://www.drupal.org/project/components) module), then the name of the library we want to attach (i.e. `training_theme/teaser`).

With the code above, we are telling Drupal that whenever we render the 50/50 teaser component, its library should be attached so the styles for the component can be applied.

{% hint style="info" %}
**More on Drupal Libraries**: [https://www.youtube.com/watch?v=V8hnfxSx4Ck](https://www.youtube.com/watch?v=V8hnfxSx4Ck)
{% endhint %}
