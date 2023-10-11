# Block Integration

Now it's time to begin the integration process for the 50/50 component. We are going to break things down and explain each part separately.

### Exercise: Integrate the 50/50 Teaser Block

1. Copy the documentation and classes setup from the first tab. These will be added to a wrapper div that surrounds our component.
2. Next, copy the layout and link variables from the second tab. These variables content the layout choice and link values needed for our component.
3. Finally, copy the markup from the 3rd tab that includes our teaser.twig file. Here we pass in the rest of the field values that we want to send as arguments to our component.

{% tabs %}
{% tab title="block-content--teaser.html.twig (step 1)" %}
```twig
{#
/**
 * @file
 * Default theme implementation to display a block content.
 *
 * @see template_preprocess_block_content_template()
 *
 * @ingroup themeable
 */
#}
{%
  set classes = [
    'block-content',
    'block-content--type-' ~ bundle|clean_class,
    'block-content--' ~ id,
    'block-content--view-mode-' ~ view_mode|clean_class,
    'container-fluid',
    'pt-6 pb-6 pt-lg-12 pb-lg-12',
  ]
%}
```
{% endtab %}

{% tab title="Step 2" %}
```twig
{% raw %}
{% set layout = content.field_teaser_layout|field_value|render %}
{% endraw %}

{%
  set link = {
    url: content.field_link[0]['#url'],
    text: content.field_link[0]['#title'],
    modifier:  content.field_teaser_bg|field_value|render == 'dark' ? 'btn-outline-primary' : 'btn-primary',
  }
%}
```
{% endtab %}

{% tab title="Step 3" %}
```twig
<div{{ attributes.addClass(classes) }}>
  {% raw %}
{% block content %}
    {%
      include '@training_theme/teaser/teaser.twig' with {
        title: content.field_title|field_value,
        eyebrow: content.field_eyebrow|field_value,
        summary: content.field_summary,
        link: link,
        image: content.field_media,
        modifier: content.field_teaser_bg|field_value|render == 'dark' ? 'rounded-4 shadow bg-dark text-white' : 'rounded-4',
        layout: content.field_teaser_layout|field_value|render,
      } only
    %}
  {% endblock %}
{% endraw %}
</div>
```
{% endtab %}
{% endtabs %}

### Some things to notice:

* Reason for setting variables for the fields above is that they all have several properties in addition to the actual value of the field. Setting these variables allow us to configure all their properties and their values prior to using them.
* A good practice when getting field values is to strip white space by using the `|render|trim`Twig filters, and then check that the field is really not empty (`is not empty ?`) if that's true, we print the field's value (i.e.`content.field_title`).
* We are using an `include` Twig statement to nest the 50/50 component into the block template. Using the theme's namespace, `training_theme`, we are able to point Drupal to our theme's `src/stories/components/teaser/teaser.twig` template. Thanks to the [Component Libraries](https://www.drupal.org/project/components) module and the namespace we created, we can direct Drupal to also look for Twig templates in our components directory, among other places.\
  **IMPORTANT**: If your theme name is not **training\_theme** be sure you use your theme name in the `@include` above.
* The next step is to map the `image`, `heading, and cta` fields with Drupal's equivalent of those fields. While creating the variables above was not required nor needed, having done so makes the mapping of keys to their values, much cleaner.
* Notice in the `@include` statement after the twig template path there is a keyword `with`? and at the end of the block of code there is a keyword `only` ? These are Twig's helpful keywords that make it possible to limit the fields we want to display.&#x20;

### Displaying the integrated 50/50 Teaser in Drupal

After clearing Drupal's cache and reloading the page we should see the Teaser in Drupal inheriting all the styles and markup from the component in Storybook.

_**You DID IT!**_ 🙌 🔥

Just for fun, once the teaser displays in Drupal, inspect the code again and you should see all the markup we wrote when we built the component in Storybook. This means Drupal is only providing the data for the component, but the markup, styles and javascript, if any, is sourced from Storybook.

## But wait ...How does Drupal get the CSS?

The answer is Drupal Libraries. Our Ignite theme generator provides library definitions that pull in our component CSS into Drupal where it can then be aggregated and rendered onto the page. Let's learn more how this all works next.
