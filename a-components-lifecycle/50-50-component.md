# 50/50 Component

The 50/50 is a more complex component because it contains more fields, logic and it also makes use of previously built components. With the 50/50 Teaser we will reuse other components by using Twig's [include](https://twig.symfony.com/doc/2.x/tags/include.html) statements. More on this later.

Whether you are building simple or complex components, the process for getting started is the same; create files for data, markup and styles. Let's do this with the 50/50 component.

First let's take a look at how this component looks so we can identify the different data fields we need.

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-20 at 12.06.11 PM.png" alt=""><figcaption><p>50/50 component</p></figcaption></figure>

Based on the design above, we need the following fields:

* **Image**
* **Eyebrow**
* **Title or heading**
* **Summary**
* **Call to action (CTA)**

## Exercise: Build the 50/50 teaser component

### Component's stock content

1. Delete the existing "teaser" folder inside of components (we are going to recreate it from scratch!)
2. Inside _components_ create a new folder called **teaser**
3. Inside the _teaser_ folder create a new file called **teaser.stories.js**
4. Inside _teaser.json_ add the following code:

{% tabs %}
{% tab title="teaser.stories.js (step 1)" %}
```javascript
import "./teaser.scss";
import TeaserTemplate from "./teaser.twig";

export default {
  title: "Editorial/50-50 Teaser",
  argTypes: {
    title: {
      description: "Teaser title",
      control: "text",
    },
    authored_date: {
      description: "Teaser authored date",
      control: "text",
    },
    image: {
      description: "Teaser image markup",
      control: "text",
    },
    summary: {
      description: "Teaser summary",
      control: "text",
    },
    link: {
      description: "Teaser read more link",
      control: "text",
    },
    layout: {
      description: "Teaser layout",
      control: "text",
    },
    modifer: {
      description: "Teaser modifier",
      control: "text",
    },
  },
};
```
{% endtab %}

{% tab title="Step 2" %}
```javascript
export const Left = TeaserTemplate.bind({});
Left.args = {
  "title": 'News Title',
  'eyebrow': 'Eyebrow',
  "image": "<img src='https://via.placeholder.com/800x600.png' class='img-fluid rounded' alt='Placeholder' />",
  "summary": 'Contra legem facit qui id facit quod lex prohibet. Nec dubitamus multa iter quae et nos invenerat. Praeterea iter est quasdam res quas ex communi. Lorem ipsum dolor sit amet, consectetur adipisici elit.',
  "link": {
    "url": "#",
    "text":"Read More",
    "modifier": "btn-primary"
  },
  "layout": "left",
  "modifier": "container-fluid rounded",
};

export const Right = TeaserTemplate.bind({});
Right.args = {
  "title": 'News Title',
  'eyebrow': 'Eyebrow',
  "image": "<img src='https://via.placeholder.com/800x600.png' class='img-fluid rounded' alt='Placeholder' />",
  "summary": 'Contra legem facit qui id facit quod lex prohibet. Nec dubitamus multa iter quae et nos invenerat. Praeterea iter est quasdam res quas ex communi. Lorem ipsum dolor sit amet, consectetur adipisici elit.',
  "link": {
    "url": "#",
    "text":"Read More",
    "modifier": "btn-primary"
  },
  "layout": "right",
  "modifier": "container-fluid rounded",
};

```
{% endtab %}
{% endtabs %}

Similar to the previous example involving the basic component, we are employing JavaScript to import files, specify the arguments of the component, and incorporate stock or dummy content into it. Our objective in this case is to enhance code efficiency and facilitate maintenance by nesting pre-existing components within the 50/50 teaser. By doing so, we can avoid code duplication and establish a single source of code for improved component management.

{% hint style="info" %}
We introduced a modifier parameter that proves useful when we want to provide custom CSS classes to the component for styling purposes.
{% endhint %}

### Component's Markup

Now let's write some HTML for the component.

1. Inside the teaser folder create a new file called **teaser.twig**
2. Inside `teaser.twig` add the following code:

{% tabs %}
{% tab title="teaser.twig" %}
```php
{{ attach_library('training_theme/teaser') }}

<div class="teaser {{ modifier }}">
  <div class="row {{ layout == 'right' ? 'flex-lg-row-reverse' : 'flex-lg-row' }} justify-content-around">
    <div class="col-lg-6 col-xxl-5">
      {{ image }}
    </div>
    <div class="col-lg-6 col-xxl-5 pt-6">
      {% raw %}
{% if eyebrow %}
        <div class="text-uppercase mb-2">
          {% include '@ignite_theme/badge/badge.twig' with {
              tag: eyebrow,
              modifier: 'text-bg-secondary'
            } only %}
        </div>
      {% endif %}
      {%
        include '@ignite_theme/heading/heading.twig' with {
          "heading": {
            title: title,
            heading_level: '2',
            modifier: ''
          }
        } only
      %}
      <div class="mt-2 mb-5">
        {% if summary %}
          {{ summary }}
        {% endif %}
      </div>
      <div class="d-grid gap-2 d-md-flex justify-content-md-start">
        {% if link.url %}
          {% include '@ignite_theme/button/button.twig' with {
            "button": {
              "url": link.url,
              "text": link.text ? link.text : 'Read more'|t,
              "icon": 'arrow_right_alt',
              "modifier": link.modifier
            }
          } only %}
        {% endif %}
{% endraw %}
      </div>
    </div>
  </div>
</div>
```
{% endtab %}
{% endtabs %}

#### Some things to notice:

* We are using the Bootstrap row and col classes to arrange our content into columns. Bootstrap also lets us specify specific breakpoint classes (e.g. col-lg-6) for our column sizes.
* We have added a conditional for the direction of the image and copy: `{{ layout == 'right' ? 'flex-lg-row-reverse' : 'flex-lg-row' }}`. Bootstrap has a class that easily allows us to reverse the direction of our columns.
* **Lastly, and most important**, we make use of Twig's `include` statement to include or nest the Badge, Heading and Button components into the 50/50 teaser. This is extremely powerful and we will be talking more about it later. Biggest benefit of include statements is that we can reuse other components to avoid duplicating code.

### Component's styles

1. Inside the _teaser_ folder create a new file called **teaser.scss**
2. Inside `teaser.scss` add this code:

{% tabs %}
{% tab title="teaser.scss" %}
```sass
// Import card styles.
@import '../card/card';

// Make the image fill the entire teaser.
.teaser img {
  object-fit: cover;
  height: 100%;
  width: 100%;
}
```
{% endtab %}
{% endtabs %}

Notice how little CSS we have added, thanks to Bootstrap's built-in classes. We are importing the card stylesheet which is used by our 50/50 component. The only change we have made here is to make the teaser image stretch as a 'cover.'

### Compiling the code

If Storybook is running you should see the Teaser component in Storybook under the Editorial category on the left side. Otherwise run the command below:

```
npm run storybook
```

In your browser of choice open the following URL: [http://localhost:6006/](http://localhost:6006/). This will open Storybook where you can find the 50/50 component under "Editorial."
