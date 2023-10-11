# Fonts & Icons

Out-of-the-box, the theme generator uses Google Fonts and Material Icons for font and icon display. To make changes to these fonts there are a few files you will need to modify in your theme.

The first placed you will need to make changes is in the Storybook preview head located at `/.storybook/preview-head.html` in your theme folder. This will make sure that the correct fonts libraries are loaded within Storybook.

{% tabs %}
{% tab title="preview-head.html" %}
```markup
<!-- Icons -->
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&display=swap" />

<!-- Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:ital,wght@0,400;0,500;0,600;1,400;1,500;1,600&display=swap" rel="stylesheet">

...
```
{% endtab %}
{% endtabs %}

For Drupal, any changes to font or icon libraries need to be made in the theme root \*.libraries.yml file.

{% tabs %}
{% tab title="training_theme.libraries.yml" %}
```yaml
...

fonts:
  css:
    component:
      //fonts.googleapis.com/css2?family=Work+Sans:ital,wght@0,400;0,500;0,600;1,400;1,500;1,600&display=swap: {
        type: external,
        minified: true
      }

icons:
  css:
    component:
      //fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&display=swap: {
        type: external,
        minified: true
      }

...
```
{% endtab %}
{% endtabs %}

In the `html.html.twig` file located at `/src/templates/layout/html.html.twig`, you will see that we pre-connect to Google font and icon APIs in order to help the assets load more efficiently on page load.

{% tabs %}
{% tab title="html.html.twig" %}
```html
...

{# Ignite: preconnect to Google Fonts API #}
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

...
```
{% endtab %}
{% endtabs %}

Finally for fonts any changes you make to the font family will need to be made in the `variables.scss` file located at `/src/stories/global/_variables.scss`.

{% tabs %}
{% tab title="_variables.scss" %}
```scss
...

// Typography
//
// Font, line-height, and color for body text, headings, and more.

// scss-docs-start font-variables
// stylelint-disable value-keyword-case
$font-family-sans-serif:      'Work Sans', sans-serif !default;
$font-family-monospace:       SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace !default;
// stylelint-enable value-keyword-case
$font-family-base:            var(--#{$prefix}font-sans-serif) !default;
$font-family-code:            var(--#{$prefix}font-monospace) !default;

...
```
{% endtab %}
{% endtabs %}

For icons, the Ignite generated theme uses a handful of icons in various Twig component files. You will need to search for the class `material-symbols-outlined` to find any references to icons, should you need to make changes to icons.
