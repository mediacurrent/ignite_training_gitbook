# Block view modes

### Reviewing the Teaser View Mode Display

Before we get into frontend integration we want to review how our fields are configured by default in Ignite. To review this on your local Drupal instance go to Admin..Structure..Block layout..Block types, then "Manage display" for the 50/50 teaser block. This will show you the display configuration for this block type.

<figure><img src="../../.gitbook/assets/Screen Shot 2023-06-21 at 3.00.04 PM.png" alt=""><figcaption><p>Manage display for Teaser block</p></figcaption></figure>

A couple of things to note:

1. For the Teaser layout and background fields we are using the "key" value which is more reliable for conditionals since it will not change.
2. For media entities we almost always use "Rendered entity" and then select the view mode for that entity. Ignite has several view modes configured for media.

Now that we have reviewed our block display configuration, next let's look at the "Medium" view mode display for our media field.
