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
| Author | field\_author | Paragraph Reference Revision |
| Call To Action | `field_cta` | Link |

For the Image field, set the following configuration:

* **Media type**: `image`

For the Tags field, set the following configuration:

* **Allowed number of values**: _Unlimited_
* **For Reference Type** select **Tags** as the Vocabulary

For the Author field, set the following configuration:

* **Allowed number of values** is 1
* **Reference type** is Author

