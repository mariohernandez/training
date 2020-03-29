# Blog content type

Before we can integrate our new Card component, we need to build a Drupal entity the same way we did for the Hero and Quote.  However, this entity is not going to be a paragraph type.  As we saw in the card component, each card item represents a node, possibly a blog post.  So we are going to build a new content type, Blog, with the same fields as the Card component.

{% tabs %}
{% tab title="Blog Content Type" %}
* From Drupal's Admin Toolbar, click **Structure \| Content Types**
* Click the **Add content type** button
* Assign the Label and Machine name below

  | Label | Machine name |
  | :--- | :--- |
  | Blog | `blog` |

* Click the **Save and manage fields** button

Add the following fields and settings to the content type:

**NOTE:**: The **Title** and **Body** fields are automatically added when a content type is created.  Keep them.

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Title | `label` | **This** **field is auto generated.  No need to create it** |
| Body | `body` | **This field is auto generated.  No need to create it** |
| Date | `field_date` | Date |
| Image | `field_image` | Media Reference |
| Tags | `field_tags` | Taxonomy Term Reference |

For the Image field, set the following configuration:

* **Media type**: `image`

For the **Tags** field, set the following configuration:

* **Allowed number of values**: _Unlimited_
* **Reference method**: _Default_
* _Check the box for_ **Create referenced entities if they don't already exist**
* _**Vocabulary**:_ Tags 
{% endtab %}
{% endtabs %}



