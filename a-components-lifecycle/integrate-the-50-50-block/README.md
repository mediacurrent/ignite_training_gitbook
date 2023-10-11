---
description: >-
  Now that we have our test layout page set up with Teaser block, let's
  integrate with the 50/50 Component that we created earlier in Storybook.
---

# Integrate the 50/50 Block

### Twig template suggestions

[Template suggestions](https://www.drupal.org/docs/8/theming/twig/working-with-twig-templates) are Twig templates used to override Drupal core or contrib modules templates. Template suggestions can be saved in a variety of places within the theme folder. If Drupal finds twig templates in the theme it uses those over the ones in core when rendering content. Template suggestions are what we will use to integrate components with Drupal. These template suggestions in the context of component integration, are typically referred to as **Presenter Templates** and as you will see, their only purpose is to pass data from Drupal to the component. They act as the middleman between Drupal and Storybook components.

### Identifying template suggestions

If you have been using Drupal for a while you may be well familiar with where to get templates from or what to name them. However if you've never worked with template suggestion no worries, Twig debugging, which [you should have enabled](https://www.drupal.org/node/2598914) in the previous page, will help us identify the templates we need.

### Examples of Twig template suggestions

Template suggestions can be generic or extremely specific depending on the task at hand. Below are two examples of naming conventions for template suggestions; one for **Node types** and the other for **Block types**.

{% tabs %}
{% tab title="node" %}
```
node--[nodeid]--[viewmode].html.twig
node--[nodeid].html.twig
node--[content-type]--[viewmode].html.twig
node--[content-type].html.twig
node--[viewmode].html.twig
node.html.twig
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="paragraph" %}
```
block-content--[block-type]--[viewmode].html.twig
block-content--[block-type].html.twig
block-content--[viewmode].html.twig
block-content.html.twig
```
{% endtab %}
{% endtabs %}

