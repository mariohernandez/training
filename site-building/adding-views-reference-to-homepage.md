# Adding Blog Lists to the Homepage

Let's add two new fields to the Homepage content type.  These will be views reference fields in order to display the blocks we created in the Blog posts view.

Be sure to enable the **Views reference field **module before proceeding.

1. From drupal’s admin toolbar, click **Structure | Block layout**
2. Scroll down and click the **Place block** button next to Content (this is the content region)
3. From the Place Block modal window look for a block called **Featured Content **(this is why it is important to name your blocks properly so they are easy to find).  If we didn’t do this when we created the blocks we would see names like **blocks\_1** or **block\_2**, which is not clear which block they might be.
4. Click the **Place block** button next to the Featured Content block
5. From the **Configure Block** modal window, set the following settings:
   1. Check Display title (this will display the title we assigned to the view block display. This is also why it is important to add the corresponding titles to your blocks when creating them in views)
   2. For Items per block choose 2 (we’re displaying two posts as featured content)
   3. Under visibility, click **Pages** and type `<front>`.  This means we only want the blocks to show in the homepage and no other pages.
   4. Click the **Save** block button
   5. Once you are back on the block layout page, drag the Featured Content block under the Main page content block.  This way the blog post will display under the hero.

#### Repeat the steps with the From our blog block

* Follow the steps above but this time using the From our blog block.  Change the number of items to display to 4.  Also, make sure the Feature Content block is above the From our blog block in the block layout page.
* After you complete the above steps, scroll down the page and click the **Save blocks** button. Now you should see a series of blog posts displayed on the homepage.  
* If you haven’t already, edit two of the blog posts and under the PROMOTION OPTIONS fieldset, check the **Promote to the front page** checkbox.  This will make it possible for Featured content posts to be displayed on the homepage.

The posts are not styled and don’t look too presentable but we will take care of this in future chapters.

