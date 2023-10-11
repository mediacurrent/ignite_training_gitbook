# Create a Basic Component

Following the Component-based design methodology we are going to build a "General" component that be reused by other components.

At a minimum most components will need the following files:

| File type     | Purpose                         |
| ------------- | ------------------------------- |
| `.twig`       | Component's HTML and Twig logic |
| `.scss`       | Component's styles              |
| `.stories.js` | Component's stock content       |

Some components may also include:

| File type | Purpose                          |
| --------- | -------------------------------- |
| `.js`     | Component's interactive behavior |

### Exercise: Building a "Collapse" component

For this exercise we will integrate Bootstrap's [Collapse feature](https://getbootstrap.com/docs/5.2/components/collapse/) which is a component that ships with Bootstrap but is not provided out of box with our theme generator.

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-14 at 11.10.20 AM.png" alt=""><figcaption><p>Bootstrap 5 Collapse component</p></figcaption></figure>

### Component's Markup

First, let's write some HTML that we will need for our new component.

{% hint style="info" %}
**NOTE:** All components will be created inside `src/stories/components`.

On a typical Drupal project the full path may look something like this: `<project-root>/web/themes/custom/<your-theme-name>/src/stories/components/`
{% endhint %}

1. Inside _components_ create a new folder called **collapse**
2. Inside the _collapse_ folder create a new file called **collapse.twig**
3. Add the following code to `collapse.twig`:

```twig
<p>
  <a class="btn btn-primary" data-bs-toggle="collapse" href="#{{ id }}" role="button" aria-expanded="false" aria-controls="collapseExample">
    {{ button_text }}
  </a>
</p>
<div class="collapse" id="{{ id }}">
  <div class="card card-body">
    {{ body }}
  </div>
</div>
```

We made modifications to the example code provided on the Bootstrap website by including a button and a collapsible content area. There are three variables required for our implementation: one for the button text, another for the copy within the collapsed content body, and the third for the ID that links the button to the collapsed element.

### Component's stock content

Next, we are going to define the story for our component and include some sample content.

1. Inside the _collapse_ folder create a new file called **collapse.stories.js**
2. Inside _collapse.stories.js_ add the following code:

```javascript
import CollapseTemplate from "./collapse.twig";

export default {
  title: "General/Collapse",
  argTypes: {
    body: {
      description: "Define the collapse body text.",
      control: "text",
    },
    button_text: {
      description: "Define the button text.",
      control: "text",
    },
    id: {
      description: "Define the collapse ID.",
      control: "text",
    }
  }
};

export const Collapse = CollapseTemplate.bind({});

Collapse.args = {
  "button_text": "Click Me!",
  "body": "Some placeholder content for the collapse component. This panel is hidden by default but revealed when the user activates the relevant trigger.",
  "id": "collapseExample"
};
```

Within this code, we begin by importing our Twig file. Next, we proceed to define the argument types and provide specific example content for our component.

### Seeing the Component in action

As soon as you save your changes in Storybook you will instantly see updates in the Storybook application (e.g. [http://localhost:6006/](http://localhost:6006/)).

### Adding CSS

You probably noticed that we creating this component witout any custom CSS, and that's exactly why we like Bootstrap. You will find that a lot of components can be created by only using Bootstrap markup. That being said, lets go ahead and add a starter CSS file.

1. Create `collapse.scss` in your `collapse` folder.
2. Add the lines below (first tab) to your new file in order to be able to use Bootstrap mixins and variables.
3. Add the import statement below to the top of the `collapse.stories,js` (second tab).

{% tabs %}
{% tab title="collapse.scss" %}
```scss
// Import site utilities.
@import '../../global/bootstrap-init';

```
{% endtab %}

{% tab title="collapse.stories.js" %}
```twig
import "./collapse.scss";

...
```
{% endtab %}
{% endtabs %}

Once you have saved your files, you can verify for any errors by checking Storybook. That concludes the current steps. In the future, we will explore how to incorporate this CSS as a Drupal theme library.
