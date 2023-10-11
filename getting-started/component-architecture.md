# Component Architecture

We recommend grouping components or stories in individual folders within your Drupal theme. This will help you keep your code organized and reusable. Each component will be self-contained, with all of its code and assets in a single folder. This will make it easy to find and reuse components, and it will also make your code easier to maintain.

```
+
|--src
|  |--stories
|     |--components
|        |--card
|           |-- card.stories.js
|           |-- card.scss
|           |-- card.twig
+
```

A component is typically broken down in four parts:

* **Markup**: Markup or HTML for a component is written in [Twig templates, Drupal 10's templating engine](https://www.drupal.org/docs/theming-drupal/twig-in-drupal).&#x20;
* **Format**: Component Story Format (CSF) is the recommended way to write stories. It's an open standard based on ES6 modules that is portable beyond Storybook.
* **Styles**: These are written in CSS or SCSS.
* **Behavior/interaction**: The component's behaviors are usually handled with JavaScript. Most components don't need JavaScript.
