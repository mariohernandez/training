# Blog content type

We'll build a new content type which we will use to build blog articles.  Blog articles are the content we will display on the homepage as Featured Content and From our Blog.  This means each card in the homepage represents a blog article in a compact view.  We will achieve the Card and Card Wide displays using Drupal's View Modes.  More on view modes shortly.

1. From Drupal's Admin Toolbar, click **Structure \| Content Types**
2. Click the **Add content type** button
3. In the _name_ field type **Blog**
4. Click the **Publishing Options** tab in the Vertical Tabs options
5. Under **Default options** leave **Published** checked.  All other check boxes should **not be checked**.
6. Click the **Save and manage fields** button at the bottom of the page

#### Add the following fields:

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Title | `label` | **This** **field is auto generated.  No need to create it** |
| Body | `body` | **This** **field is auto generated.  No need to create it** |
| Date | `date` | **This** **field is auto generated.  No need to create it** |
| Image | `field_blog_image` | Media Reference |
| Tags | field\_blog\_tags | Taxonomy Term Reference |
| Author | field\_author | User Reference |
| Category | field\_category | Text \(plain\) |

{% hint style="info" %}
**NOTE**: We don't need to add a `title` , `date`, or `body` fields since these already come out of the box on any content types.
{% endhint %}

For the Image field, set the following configuration:

* **Media type**: `image`

For the Tags field, set the following configuration:

* **Allowed number of values**: _Unlimited_
* **Reference method**: _Default_
* _Check the box for_ **Create referenced entities if they don't already exist**
* _**Vocabulary**:_ Tags

For the Author field, set the following configuration:

* **Allowed number of values** is 1
* **Reference type** deselect _Include the anonymous user_

