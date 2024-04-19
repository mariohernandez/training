# View modes

## Why view modes?

Most of the content in our site is driven by Blog articles. However, articles are being displayed in different ways. The _Featured Content_ section shows articles differently than _From our Blog_. By "_different_" we don't mean they look different visually (which they do), but the fields displayed in each of the two sections vary. There are common fields such as the image, title, and body, but there are also fields that are unique to each section. Once we get into a full blog node, things look even more different.

There are many ways to manage how the same type of content can be displayed differently depending on the requirements, but one very effective way is to use Drupal's [View Modes](https://www.drupal.org/node/2511722#s-view-modes-and-view-displays). View modes allows us to control the fields we want to display on different areas of our website. We are going to setup 3 different view modes: **Full content**, **Featured**, and **Teaser**. Each of these 3 view modes can be configured to display different fields.

### Here's our plan with these view modes:

| View mode        | Purpose                                                                                                          |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Default**      | This will remain untouched so it can serve as template for new view modes we may create in the future            |
| **Full content** | This will be used when displaying the full node of a blog post (detailed page)                                   |
| **Featured**     | This view mode will be used by the Card Wide variant to build the **Featured Content** section in the homepage   |
| **Teaser**       | This view mode will be used by the regular Card component to build the **From our blog** section in the homepage |

## Manage fields with view modes

Managing fields with view modes ensures we are letting Drupal do things the way Drupal like to do things for rendering content. Then through the use of twig template suggestions per each view mode we integrate the components we want to use to render our content.

1. While still in the **Article** content type, click **Manage display**
2. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
3. Click the **Manage view modes** link
4. Under the Content section click the **Add new Content view mode** link
5. Type **Featured** in the name field and click the **Save** button
6. Return to the Article content type **Manage display** screen
7. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
8. Ensure **Full Content**, **Featured**, and **Teaser** are checked and press the **Save** button

## Configure the Featured view mode

1. While still in the Article content type, click **Manage display**
2. Click the **Featured** view mode
3. Drag the **Tags** and **Links** fields into the **Disabled** section.  Tags are not needed in Card Wide.
4. For the Author field change its format to **Rendered entity**
5. Change each of the field's labels to **Hidden**
6. For the **Body** field, change the Format to **Trimmed** and change the **Trim limit** to 125 characters by clicking the cogwheel icon to the right of the body field
7. Click the **Update** button
8. We'll comeback to configuring the image field with the right image styles later on
9. Click the **Save** button

## Teaser view mode

1. Repeat all the steps above for the **Teaser** view mode except on step 3, drag the **Author, Category**, and **Links** into the **Disabled** section
2. For the Tags field, change its format to be **Rendered entity**
3. For step 4 above, trim the body text to 160 characters
4. Click the **Save** button

## **Full content view mode**

1. Hide the labels of all the fields
2. For the Tags and Author fields change their format to **Rendered entity**
3. Save your changes
