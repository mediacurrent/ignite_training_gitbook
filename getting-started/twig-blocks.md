# Twig Blocks

## What are Twig Blocks?

Twig blocks serve a dual purpose in Drupal, acting as both placeholders and replacements. They can be likened to empty spaces waiting to be filled within a Drupal page or regions within your pages.

The challenge we encounter is finding the right balance between controlling the markup and adhering to Drupal's recommended practices for content rendering. When it comes time to integrate a Storybook component with Drupal, we often rely on `include` statements, which generally suffice. However, there are instances where we need to modify content or markup before Drupal renders a component, and `include` statements do not provide this flexibility. While `extends` statements could be an option, they may also have limitations in certain scenarios. In such cases, the ideal approach is to employ Twig's `embed` statements. Embed statements combine the functionalities of both `include` and `extends` statements, providing a more versatile solution.&#x20;

Let's explore using the Accordion component that is rendered from the theme generator.

{% tabs %}
{% tab title="accordion.twig" %}
```twig
{{ attach_library('training_theme/accordion') }}

<div class="{{ modifier }}">
  <div class="accordion">
    {% raw %}
{% block accordion_items %}
      {% for item in items %}
        {%
          include '@ignite_theme/accordion/accordion-item.twig' with { item: item } only
        %}
      {% endfor %}
    {% endblock %}
{% endraw %}
  </div>
</div>
```
{% endtab %}

{% tab title="accordion-item.twig" %}
```twig
<div class="accordion-item rounded mb-3 border-0">
  <h2 class="accordion-header" id="heading{{ item.accordion_instance }}">
    <button class="accordion-button text-dark rounded collapsed p-3 pt-4 pb-4 fs-5 fw-semibold" type="button" data-bs-toggle="collapse" data-bs-target="#collapse{{ item.accordion_instance }}" aria-expanded="false" aria-controls="collapse{{ item.accordion_instance }}">
      {{ item.heading }}
    </button>
  </h2>
  <div id="collapse{{ item.accordion_instance }}" class="accordion-collapse collapse" aria-labelledby="heading{{ item.accordion_instance }}">
    <div class="accordion-body">
      {% raw %}
{% block accordion_content %}
        {{ item.content }}
      {% endblock %}
{% endraw %}
    </div>
  </div>
</div>
```
{% endtab %}
{% endtabs %}

Within the `accordion.twig` template, we have defined a Twig block called `accordion_items`. On its own, this block does not have any functionality. The purpose of including this block is to allow for the integration of accordion items using a separate paragraphs presenter template.

{% hint style="warning" %}
**IMPORTANT:** Twig blocks are not the same, or have anything to do with Drupal blocks.
{% endhint %}

{% tabs %}
{% tab title="block-content--accordion.html.twig" %}
```twig
...
<div{{ attributes.addClass(classes) }}>
  ...
  {% raw %}
{% block content %}
    {% embed '@training_theme/accordion/accordion.twig' with { content: content, modifier: "container-fluid" } only %}
      {% block accordion_items %}
        {{ content.field_accordion_item }}
      {% endblock accordion_items %}
    {% endembed %}
  {% endblock %}
{% endraw %}
</div>
```
{% endtab %}

{% tab title="paragraph--accordion-item.html.twig" %}
```twig
{% embed '@training_theme/accordion/accordion-item.twig' with {
  "item": {
    "heading": content.field_title|field_value,
    "accordion_instance": paragraph.id(),
  },
  "content": content
} only %}
  {% raw %}
{% block accordion_content %}
    {{ content.field_body }}
    {{ content.field_link }}
  {% endblock %}
{% endembed %}
{% endraw %}
```
{% endtab %}
{% endtabs %}
