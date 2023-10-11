# Integrating the 50/50 component

### Exercise: Creating twig templates for blog posts

1. In your Drupal site, navigate to "Recent Blogs" (i.e. /recent-blogs)
2. Right-click on any of the Blog posts articles and select **Inspect** or **Inspect Element**
3. Scroll up in the inspector's code until you find the `<article>` element that wraps the entire article you clicked on.  There may be multiple `<article>` tags within each article, but ensure you are looking at the main article wrapper.  See screenshot below (click on it to zoom in):

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-26 at 1.26.57 PM.png" alt=""><figcaption><p>Screenshot of a rendered article being inspected</p></figcaption></figure>

* **THEME HOOK:** Tells you what entity you are currently looking at.  In this example we are looking at the **node**, which is what we want since we are trying to configure the Blog nodes with the right component.
* By examining the template suggestion names, we can easily identify that we are dealing with a node. All the template suggestions for this entity type start with the word "**node--\***". This naming convention provides us with the flexibility to be as specific or general as required, allowing us to target the desired template for customization.
* Current we are using the default node template provided by the Stable9 base theme. We want to create a more specific presenter template that will integrate node teasers with out 50/50 teaser component.

{% hint style="info" %}
**IMPORTANT:** To ensure we are all following along with the same article type, please ensure you selected an article from the _Recent blogs_ view. This means you should see the word `teaser` somewhere in the list of template names above.
{% endhint %}

#### Creating a template for the node teaser view mode

The focus at this point is to create template suggestions for all nodes that will be displayed in the **Teaser** view mode. We could target article nodes specifically but instead we are going to apply this integration to all nodes. If we change our minds later we can always rename the template to a more specific article teaser suggestion.

1. Create a new template named `node--teaser.html.twig` in your teaser templates folder at `/themes/custom/training_theme/src/stories/components/teaser/templates/`.
2. Add a word like TEST so that you will be able to verify Drupal picked up the new template suggestion next time you clear caches.
3. Clear your Drupal's cache.
4. Reload the page and verify that you can see your new custom template.

### Integrating the 50/50 component

OK, now that our custom twig template is ready, it's time to plug it to our 50/50 component so our blog posts look styled.

Open **node--teaser.html.twig** in your editor and replace your code with the following code.

{% tabs %}
{% tab title="node--teaser.html.twig" %}
```twig
{#
/**
 * @file
 * Theme override for the "teaser" view mode.
 */
#}
{%
  set classes = [
    'node',
    'node--type-' ~ node.bundle|clean_class,
    node.isPromoted() ? 'node--promoted',
    node.isSticky() ? 'node--sticky',
    not node.isPublished() ? 'node--unpublished',
    view_mode ? 'node--view-mode-' ~ view_mode|clean_class,
  ]
%}
<div{{ attributes.addClass(classes) }}>
  {{ title_prefix }}
  {{ title_suffix }}

  {%
    include '@training_theme/teaser/teaser.twig' with {
      title: label,
      eyebrow: content.field_eyebrow,
      summary: content.field_summary,
      link: url,
      image: content.field_thumbnail,
      layout: 'left',
      modifier: 'rounded-4 mb-6 mb-lg-12',
    } only
  %}
</div>
```
{% endtab %}
{% endtabs %}

#### Some things to notice:

1. Similar to our block teaser we have added some wrapper markup and the title prefix/suffix variables for contextual links
2. Many of the field mappings look the same as our block entity because our node uses fields of the same name as our "Teaser" block.

### Rendering our updated teasers

Now that the teaser integration is complete, let's take a look at how the blog nodes look in Drupal.

1. After saving all your changes to **node--teaser.html.twig**, clear Drupal's cache
2. Reload the page.

After loading the page you should see blog teasers rendered using our 50/50 component template.

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-26 at 2.57.26 PM.png" alt=""><figcaption><p>Recent Blogs page teaser screenshot</p></figcaption></figure>

Now our page is complete and should also render contextual links when you hover over a node teaser.
