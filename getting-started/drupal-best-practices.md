# Drupal Best Practices

## Presenter templates

Presenter templates are Twig template suggestions in a theme (e.g., `node--news.html.twig`, `block--card.html.twig`, `field--something.html.twig`, etc.), but in the context of Component-based development, their only purpose is to pass data from Drupal to the component. This means everything related to the component such as Markup, CSS and Javascript is done at the component level in Storybook, and when it’s time to wire the component with Drupal, we use the appropriate presenter template, or Twig template suggestion, to simply map Drupal fields with the component's fields we defined in Storybook.

There are other ways to integrate components with Drupal, such as the [UI Patterns](https://www.drupal.org/project/ui\_patterns) module, pre-processing, but the most popular approach is presenter templates.

## Presenter templates best practices

* It’s best to try to follow a component-based design approach that takes advantage of reusable components within the design system.
* Twig **blocks** (not the same or related to Drupal blocks) can be helpful for allowing embeds of smaller components.
* Let Drupal render all fields at the theme level with little to no pre-processing. Use view modes as much as possible.
* Use modules that extend twig ([twig field value](https://www.drupal.org/project/twig\_field\_value), [twig tweak](https://www.drupal.org/project/twig\_tweak), etc.) when only the field value is required.
* Create twig template files to help remove bloated field markup, and make use of twig’s extends statements to help streamline reuse of field templates.

## Benefits of this approach

* It’s (mostly) twig, scss/css, Javascript, with no PHP.
* Although you may end up with lots of twig template files, you can set up a directory structure that (hopefully) helps keep them logically organized, and easier to see how things piece together.

## Passing fields values to components

In the presenter template method you'll quickly discover that when passing the value of a field to your component, Drupal does not give us the raw value of that field, we're instead given a [render array](https://www.drupal.org/docs/8/api/render-api/render-arrays), and when that array is rendered, it includes a lot of default markup that will often get in the way. While we may be tempted to just pluck the value that we want from the render array and pass it to our component, it's best to try and let Drupal fully render the field to avoid cache invalidation issues. We will see examples of this as we build components.
