# Include statements

The `include` statement includes or nests a twig template (components, node, blocks, etc), and returns the rendered content of that file.

An example of an typical `include` statement looks like this:

```php
{% raw %}
{% include 'header.html' %}
{% endraw %}
```

Include statements accept a path parameter to the file you want to include.

## Includes in context of Drupal components

In a Drupal theme, include statements are mainly used to nest components into other components or templates. This is powerful because by including a component we avoid duplicating code. As we saw in the 50/50 component, we were able to include previously built components and leverage all the work we did with those components without repeating ourselves. Because the Badge, Heading and Button components were built in such a way, they still provide a mechanism for us to change them while being included so they meet our needs per use case.

### Let's review the Heading include in the 50/50 Teaser

{% tabs %}
{% tab title="teaser.twig" %}
```php
{%
  include '@training_theme/heading/heading.twig' with {
    "heading": {
      title: title,
      heading_level: '2',
      modifier: ''
    }
  } only
%}
```
{% endtab %}
{% endtabs %}

* The include statement above uses a relative path. This was done by creating a theme namespace (training\_theme), which is mapped to `src/stories/components/`, then we complete the path by providing the template name for the component. The keyword with allows to pass additional variable to an include (i.e. heading)
* The keywords `with` and `only` restrict access to the context of the component. For example, if a component has multiple variables we can opt to only pass some of them in the include.

Being able to customize components during the "include" process is a must. There are two ways we can change variables, properties, or values of a component. Let's use the 50/50 Teaser as an example:

1. In `teaser.stories.js` we could change the `heading_level`, `modifier`, or `title` to the values we need.
2. We could make the changes directly in the `include` as follows:

{% tabs %}
{% tab title="teaser.twig" %}
```php
{%
  include '@training_theme/heading/heading.twig' with {
    "heading": {
      "title": "A new title here",
      "modifier": 'some-css-class',
      "heading_level": "3"
    }
  } only
%}
```
{% endtab %}
{% endtabs %}

Being able to reuse components while still having the options to change them on the fly to meet our needs is an incredible advantage of twig includes. We will use includes throughout this training to reduce code duplication.

{% hint style="info" %}
Learn more about [Twig includes](https://twig.symfony.com/doc/3.x/tags/include.html)
{% endhint %}
