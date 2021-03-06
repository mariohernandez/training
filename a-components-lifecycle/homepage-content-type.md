# Homepage content type

### Exercise: Building a Homepage content type

We'll build a new content type which we will use to build the homepage with all of its components shown in our design.

1. From Drupal's Admin Toolbar, click **Structure \| Content Types**
2. Click the **Add content type** button
3. In the _name_ field type **Homepage**
4. Click the **Save and manage fields** button at the bottom of the page
5. Delete the **body** field

### Exercise: Adding the Hero paragraph type to the Homepage content type

1. While still in the Homepage content type, click the **Add field** button
2. Under the _Add a new field_ dropdown, scroll to the **Reference Revisions** section and select **Paragraph**

   | Label | Machine name |
   | :--- | :--- |
   | Hero | `field_hero` |

3. Click the **Save and continue** button
4. Change _Allowed number of values\__ to **Limited - 1**
5. In the _Reference Type_ section, choose **Hero** under _Paragraph type_
6. Click the **Save settings** button

### Exercise: Create a new Node with a Hero

Using the Homepage content type, create a new node and add a Hero component in it:

1. From Drupal's Admin toolbar, click **Content**
2. Click the **Add content** button
3. Select **Homepage**
4. Fill out the Page's title using **Homepage**
5. Then fill out all fields in the Hero paragraph type
6. Click the **Save** button

After saving your page the hero component should look something similar to this:

![Drupal Node with Hero Paragraph](../.gitbook/assets/d8-hero.png)

It's pretty obvious there are a lot of things that need improvement with our Hero, but we will get to that shortly.  

