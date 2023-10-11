# Drupal Attributes

When working with Drupal's twig templates, you will often come across the usage of the "attributes" variable within the template. This variable allows core and contrib modules to inject CSS classes, IDs, or data attributes into the template markup. Additionally, you may encounter the "title\_prefix" and "title\_suffix" variables, which are used by core and contrib modules to insert additional markup into twig templates. One notable example is the core Contextual Links module.

It is important to understand that removing the "attributes," "title\_prefix," or "title\_suffix" variables from a template, such as a node template, would prevent the Contextual Links module from adding its dropdown to the display of nodes. Consequently, this would disable features like inline editing of nodes or other tasks typically associated with the Contextual Links module.

Our usual recommendation is to handle the rendering of attributes, title\_\_prefix, and other Drupal-specific variables in the presenter template. By doing so, we ensure that the Storybook component solely focuses on the component's design-related markup.

Example:

```twig
{# Example Block content presenter template #}
{%
  set classes = [
    'block-content',
    'block-content--type-' ~ bundle|clean_class,
    'block-content--' ~ id,
    'block-content--view-mode-' ~ view_mode|clean_class,
    'container-fluid',
    'mb-10',
  ]
%}

<div{{ attributes.addClass(classes) }}>
  {% raw %}
{% block content %}
    {# Include Storybook component #}
    {%
      include '@ignite_theme/[story]/[component].twig' with {
        ...
    %}
  {% endblock %}
{% endraw %}
</div>
```

{% hint style="info" %}
Note that the `without` twig filter in this example is a Drupal-specific filter so it will not work inside of Storybook.
{% endhint %}
