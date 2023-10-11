# 50/50 Teaser Block

### Reviewing the Teaser Block

<figure><img src="../../.gitbook/assets/Screen Shot 2023-06-21 at 11.02.35 AM.png" alt=""><figcaption><p>Screenshot of the Teaser block field configuration</p></figcaption></figure>

Let's review how the Ignite 50/50 block fields would map to the component we have built.

<table><thead><tr><th width="164">Field</th><th>Notes</th></tr></thead><tbody><tr><td>Eyebrow</td><td>This text value will be passed to our eyebrow argument which uses a "badge" sub-component.</td></tr><tr><td>Link</td><td>This link is an optional value that will be used as a CTA on our teaser.</td></tr><tr><td>Media</td><td>The media field here is an image that is displayed on one side of the 50/50 component.</td></tr><tr><td>Summary</td><td>This is the summary text for the teaser.</td></tr><tr><td>Teaser Background</td><td>We want to support a "dark" and "light" version of the component so we will use this field value to inject a modifier class into our component.</td></tr><tr><td>Teaser Layout</td><td>We will use this layout value to determine whether we want the image to appear on the left or right side.</td></tr><tr><td>Title</td><td>This value will be used for the teaser heading.</td></tr></tbody></table>
