# Card paragraph type

Follow the stepsbelow to build a paragraph type for the Card component.

{% hint style="info" %}
**TIP:** You can reuse fields from previously created entities such as Hero paragraph type.
{% endhint %}

## Exercise: Create the Card paragraph type in Drupal

* From Drupal's Admin Toolbar, click **Structure \| Paragraph Types**
* Click the **Add paragraph type** button
* Assign the Label and Machine name below

  | Label | Machine name |
  | :--- | :--- |
  | Card | `card` |

* Click the **Save and manage fields** button

Add the following fields and settings to the paragraph type:

**NOTE:**: All fields use `1` as the **Allowed Number of values**.

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Title | `field_title` | Text \(Plain\) |
| Body | `field_body` | Text \(Plain, long\) |
| Image | `field_image` | Media Reference |
| Call To Action | `field_cta` | Link |

For the Image field, set the following configuration:

* **Media type**: `image`

For the CTA field, set the following configuration:

* **Allowed link type**: _Both internal and external links_
* **Allowed link text**: _Required_

### Putting the new paragraph type\(s\) to use

Now that the paragraph type is done, it's time to add it to a content type. Paragraph types on their own are useless. They need to be added to other entities such as a content type as an **Entity Reference** field.

### Adding the paragraph type to the Article content type

* From Drupal's Admin Toolbar, click **Structure \| Content Types**
* Click the **Manage fields** button next to **Article**
* Click the **Add field** button
* Under the _Add a new field_ dropdown, scroll to the **Reference Revisions** section and select **Paragraph**

  | Label | Machine name |
  | :--- | :--- |
  | Card | `field_card` |

* Click the **Save and continue** button
* Change _Allowed number of values\__ to **Limited - 1**
* In the _Reference Type_ section, choose **Hero** under _Paragraph type_
* Click the **Save settings** button

We'll use the Article content type shortly to create a new Hero node.
