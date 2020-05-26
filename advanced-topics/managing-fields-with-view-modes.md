# View modes

### Why view modes?

Most of the content in our site is driven by Blog articles.  However, each section on our site, although displaying blog articles, is displayed in different ways. The _Featured Content_ shows articles differently than _From our Blog_.  By "different" we don't mean they look different visually, but the fields also vary.  Once we get into a full blog node, things look even more different.

There are many ways to manage how the same type of content can be displayed differently depending on the requirements, but one very effective way is to use Drupal's View Modes.  View modes allows us to control what fields are displayed.  We are going to setup 3 different view modes: **Full content**, **Featured**, and **Teaser**.  Each of these 3 view modes can be configured to display different fields.

#### Here's our plan with these view modes:

| View mode | Purpose |
| :--- | :--- |
| **Default** | This will remain untouched so it can serve as template for new view modes we may create in the future |
| **Full content** | This will remain untouched so it can serve as template for new view modes we may create in the future |
| **Featured** | This view mode will be used by the Card Wide variant |
| **Teaser** | This view mode will be used by the regular Card component |

### Manage view modes

Managing fields with view modes ensures we are letting Drupal do things they way Drupal like to do things for rendering content.  Then through the use of twig template suggestions per each view mode we integrate the components we want to use to render our content.

1. While still in the Blog content type, click **Manage display**
2. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
3. Click the **Manage view modes** link
4. Under the Content section click the **Add new Content view mode** link
5. Type **Featured** in the name field and click the **Save** button
6. Return to the Blog content type **Manage display** screen
7. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
8. Ensure **Full Content**, **Featured**, and **Teaser** are checked and press the **Save** button

### Configure the Featured view modes

1. While still in the Blog content type, click **Manage display**
2. Click the **Featured** view mode
3. Drag the **Tags** fields into the **Disabled** section.  Tags are not needed in Card Wide.
4. Change each of the field's labels to **Hidden**
5. For the **Body** field, change the Format to **Trimmed** and change the **Trim limit** to 100 characters by clicking the gear icon to the right of the body field
6. Click the **Update** button
7. For the **Author** field ensure its format is set to **Rendered entity** and select **Custom** as the view mode by clicking the gear to the right of the field
8. Click the **Update** button
9. We'll comeback to configuring the image field with the right image styles later on
10. Click the **Save** button

### Teaser view mode

1. Repeat all the steps above for the **Teaser** view mode except on step 3, drag the **Author** and **Category** into the **Disabled** section
2. For the image field, change its format to be **Rendered entity**
3. Click the **Save** button

### **Full content view mode**

1. Hide the labels of all the fields
2. Save your changes

