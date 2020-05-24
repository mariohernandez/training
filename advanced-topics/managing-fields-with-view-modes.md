# Managing fields with view modes

### Why view modes?

Most of the content in our site is driven by Blog articles.  However, each section on our site, although displaying blog articles, they display them in different ways. The Featured Content shows articles differently than From our Blog.  By "different" we don't mean they look different visually, but the fields also vary.  Once we get into a full blog node, things look even more different.

There are many ways to manage how the same type of content can be displayed differently depending on the requirements, but one very effective way is to use View Modes.  View modes allows us to control what fields are displayed.  In the previous exercise we setup 3 different view modes: **Full content**, **Featured**, and **Teaser**.  Each of these 3 view modes can be configured to display different fields.

Managing fields with view modes ensures we are letting Drupal do things they way Drupal like to do things for rendering content.  Then through the use of template suggestions per view mode we simply provide the components we want to use for the fields we want to render.

### Configure the Featured view modes

1. From Drupal's Admin Toolbar, click **Structure \| Content Types**
2. Click the **Featured** view mode
3. Drag the **Tags** and **Links** fields into the **Disabled** section
4. Change each of the field's labels to **Hidden**
5. For the **Body** field, change the Format to **Trimmed** and change the **Trim limit** to 100 characters by clicking the gear icon to the right of the body field
6. Click the **Update** button
7. For the **Author** field ensure its format is set to **Rendered entity** and select **Custom** as the view mode by clicking the gear to the right of the field
8. Click the **Update** button
9. Click the **Save** button

### Teaser view mode

1. Repeat all the steps above for the **Teaser** view mode except on step 3, drag the **Author** and **Links** into the **Disabled** section
2. For the image field, change its format to be **Rendered entity**

### **Full content view mode**

1. Drag the **Links** field into the **Disabled** section
2. Hide the labels of all the fields

