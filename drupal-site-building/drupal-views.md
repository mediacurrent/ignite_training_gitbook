# Drupal Views

For our next task, let's proceed with the creation of a new Drupal View called "Recent blogs" and seamlessly incorporate it with our previously developed 50/50 component.

To construct a page displaying the latest blogs, we will leverage the capabilities of Drupal's views and View Modes. By querying all the Article content, we can generate a comprehensive list of blog article posts. Through the utilization of View Modes, we have the ability to specify the fields we want to present and determine the format in which these fields will be displayed.

Drupal Views essentially allow us to construct and execute database queries using Drupal's user interface, empowering us with a flexible approach to retrieve and showcase desired data.

### Exercise: Blog articles View

Let's begin by establishing a new view to fetch all the article posts. This new view will be designed in such a straightforward manner that we can easily configure it entirely using the user-friendly Views UI add screen.

1. From Drupal's Admin toolbar click **Structure | Views**
2. Click the **Add view** button
3. For View name type **Recent Blogs**
4. Machine name should auto complete to `recent_blogs`
5. For VIEW SETTINGS, **Show** _Content_ **Of type:** _Article_
6. Check **Create a page** and leave the default settings
7. For PAGE DISPLAY SETTINGS, ensure **Teasers** is selected&#x20;
8. Leave **Use a pager** checkbox checked
9. Click the **Save and edit** button
10. Verify in the Views UI preview that you are seeing blogs rendered

Your view should look like the image below.  _Click on the image to zoom in._

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-26 at 12.50.44 PM.png" alt=""><figcaption><p>Screenshot of "Recent Blogs" view</p></figcaption></figure>

Now visit the `/recent-blogs` page in your browser. You should see something like the screenshot below:

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-26 at 1.23.15 PM.png" alt=""><figcaption><p>Unstyled Recent Blog teasers screenshot</p></figcaption></figure>

Currently, our teasers lack visual appeal as the node teaser view mode hasn't been integrated with the 50/50 component, unlike our Teaser block. As a result, we need to address this integration gap to enhance the appearance of our teasers.

