# Global styles

Learn how global Bootstrap styles are applied within Storybook.

## Bootstrap.scss

In our theme's package.json, we include the Bootstrap framework source files. Bootstrap is initialized from Storybook in a modified bootstrap.scss file created by our theme generator. The global bootstrap files are located at `src/stories/global/.`

The Ignite theme allows developers to pick and choose which bootstrap files they want to include, override or discard.&#x20;

{% tabs %}
{% tab title="bootstrap.scss" %}
```scss
@import 'bootstrap/scss/mixins/banner';
@include bsBanner('');

// Configuration
@import 'bootstrap/scss/functions';

// Use custom variables file
@import 'variables';

@import 'bootstrap/scss/maps';
@import 'bootstrap/scss/mixins';
@import 'bootstrap/scss/utilities';

// Layout & common components
@import 'bootstrap/scss/root';
@import 'reboot';
@import 'bootstrap/scss/close';
@import 'bootstrap/scss/type';
@import 'bootstrap/scss/images';
@import 'containers';
@import 'grid';
@import 'bootstrap/scss/tables';
@import 'bootstrap/scss/forms';
@import 'bootstrap/scss/transitions';
@import 'bootstrap/scss/modal';
@import 'bootstrap/scss/list-group';
@import 'bootstrap/scss/buttons';
@import 'bootstrap/scss/tooltip';

// Helpers
@import 'bootstrap/scss/helpers';

// Utilities
@import 'bootstrap/scss/utilities/api';
```
{% endtab %}
{% endtabs %}

## Bootstrap init

The bootstrap-init file is located at `src/stories/global/bootstrap-init.scss`. This file is referenced from components in order to use helper functions and variables.

{% tabs %}
{% tab title="bootstrap-init.scss" %}
```scss
@import  'bootstrap/scss/mixins/banner';
@include bsBanner(Utilities);

// Configuration
@import 'bootstrap/scss/functions';

// Use custom variables file
@import 'variables';

@import 'bootstrap/scss/maps';
@import 'bootstrap/scss/mixins';

```
{% endtab %}
{% endtabs %}

## Variables

One of the most important files to get comfortable modifying is the modified Bootstrap `_variables.scss` file located at `src/stories/global/_variables.scss`. Ignite overrides some variables out of the box. These overrides are indicated by inline comments in the file.

{% hint style="info" %}
Some variables have been moved to their appropriate component to make them easier to find (e.g. accordion related variables can be found in the accordion component.
{% endhint %}

{% tabs %}
{% tab title="_variables.scss" %}
```scss
// Variables
//
// Variables should follow the `$component-state-property-size` formula for
// consistent naming. Ex: $nav-link-disabled-color and $modal-content-box-shadow-xs.

// Color system

// scss-docs-start gray-color-variables
$white:    #fff !default;
$gray-100: #f8f9fa !default;
$gray-200: #e9ecef !default;
$gray-300: #dee2e6 !default;
$gray-400: #ced4da !default;
$gray-500: #adb5bd !default;
$gray-600: #6c757d !default;
$gray-700: #495057 !default;
$gray-800: #343a40 !default;
$gray-900: #212529 !default;
$black:    #000 !default;
// scss-docs-end gray-color-variables

...
```
{% endtab %}
{% endtabs %}

## Additional overrides

The following Bootstrap includes have a handful of overrides that required a local copy of the file in `src/stories/global/`. More than likely you will not need to make changes to these files.

1. `_containers.scss` - Ignite provides a cleaner application of nested containers (which should be avoided when possible), and applies full gutter value for containers.
2. `_grid.scss` - Ignite allows developers to specify gutter widths per breakpoint.
3. `_reboot.scss` - Ignite makes a few small overrides to this file.
