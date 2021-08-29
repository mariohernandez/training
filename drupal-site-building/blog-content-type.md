# Blog articles

We'll modify Drupal core's Article content type so we can use it to generate blog post for our site. Blog articles are the content we will display on the homepage as Featured Content and From our Blog.  This means each card in the homepage represents a blog article in a compact view.  We will achieve the Card and Card Wide displays using Drupal's View Modes.  

1. From Drupal's Admin Toolbar, click **Structure \| Content Types**
2. Click **Manage fields** next to **Article**
3. Delete the **Comments** field
4. Add the missing fields based on the table below
5. Click the **Save and manage fields** button at the bottom of the page

#### Add the following fields:

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Title | `label` | **This** **field is auto generated.  No need to create it** |
| Body | `body` | **This** **field is auto generated.  No need to create it** |
| Date | `date` | **This** **field is auto generated.  No need to create it** |
| Image | `field_image` | Media Reference |
| Tags | `field_tags` | Taxonomy Term Reference |
| Author | `field_author` | User Reference |
| Category | `field_category` | Text \(plain\) |

For the Author field, set the following configuration:

* **Allowed number of values** is 1
* **Reference type** deselect _Include the anonymous user_

