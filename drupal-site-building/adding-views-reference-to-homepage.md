# Adding Views reference to homepage

Let's add two new fields to the Homepage content type.  These will be views reference fields in order to display the blocks we created in the Blog posts view.

1. From Drupal's admin toolbar, select **Structure &gt; Content types &gt; Homepage &gt; Manage fields**
2. Click the **Add field**  button
3. From the **Add new field** dropdown, under the _Reference_ group, select **Views reference**
4. Type **Blog articles list** as the label and click the **Save and continue** button
5. Limit number of values is **1**
6. Click the **Save field settings** button
7. Under **View display plugins to allow** select **Block**
8. Under **Preselect View Options** select **Blog posts**
9. Repeat all the steps but this time use **Featured Content** for step 4

