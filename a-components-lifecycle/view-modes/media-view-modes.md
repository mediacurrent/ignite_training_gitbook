# Media view modes

When we integrate the 50/50 component we are going to want to just pass the media field and let Drupal handle all the rendering. This is considered best practice. It also makes theming much easier. Let's look at how the "Medium" display is configured since we know that the Teaser media field uses the "Medium" view mode. To view this configuration go to Admin..Structure..Media types and then select the "Manage display" option for the "Image" media type.

<figure><img src="../../.gitbook/assets/Screen Shot 2023-06-21 at 3.17.32 PM.png" alt=""><figcaption><p>The image media type "Medium" display configuration</p></figcaption></figure>

We are diving into a bit of a rabbit hole but it's important to know how the image renders onto the page in case we need to change any of the configuration. Here you see we are rendering a responsive image style for this display which is also a best practice.

Next we will look at how we have configured our responsive images.
