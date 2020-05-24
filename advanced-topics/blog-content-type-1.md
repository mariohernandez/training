# Blog content type

We'll build a new content type which we will use to build blog articles.  Blog articles are the content we will display on the homepage as Featured Content and Blog Content.

1. From Drupal's Admin Toolbar, click **Structure \| Content Types**
2. Click the **Add content type** button
3. In the _name_ field type **Blog**
4. Click the **Publishing Options** tab in the Vertical Tabs options
5. Under **Default options** on leave **Published** checked.  All other check boxes should not be checked.
6. Click the **Save and manage fields** button at the bottom of the page

#### Add the following fields:

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Image | `field_blog_image` | Media Reference |
| Tags | field\_blog\_tags | Taxonomy Term Reference |
| Author | field\_author | User Reference |
| Call To Action | `field_cta` | Link |

{% hint style="info" %}
**NOTE**: We don't need to add a `title` , `date`, or `body` field since these already come out of the box on any content types.
{% endhint %}

For the Image field, set the following configuration:

* **Media type**: `image`

For the Tags field, set the following configuration:

* **Allowed number of values**: _Unlimited_
* **For Reference Type** select **Tags** as the Vocabulary

For the Author field, set the following configuration:

* **Allowed number of values** is 1
* **Reference type** deselect _Include the anonymous user_

### Manage view modes

We need to add and enable some view modes to the Blog content type.  This will allow us to display content differently.  View modes are pretty powerful as they do the heavy lifting for managing fields to the be displayed on any page.

1. While still in the Blog content type, click **Manage display**
2. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
3. Click the **Manage view modes** link
4. Under the Content section click the **Add new Content view mode**
5. Type **Featured** in the name field and click the **Save** button
6. Return to the Blog content type **Manage display** screen
7. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
8. Ensure **Full Content**, **Featured**, and **Teaser** are checked and press the **Save** button

Here's our plan with these view modes:

* **Default**:  This will remain untouched so it can serve as template for new view modes we may create in the future.
* **Full content**:  This view mode will be used to display full blog post nodes \(detail page\)
* **Featured**: This view mode will be used by the Featured Content section which uses the Card Wide variant.
* **Teaser**: This view mode will be used by the From our Blog section which uses the regular Card component.



