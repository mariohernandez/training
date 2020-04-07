# Hero paragraph type

Using a paragraph type will allow us to reuse these components on any page we need to.

The tabbed content below provides instructions for building the Hero paragraph type.  Notice we also have the same instructions for Quote and Card components.  We will build those soon.  You will return to these instructions when is time to build those paragraph types.

{% hint style="info" %}
**TIP:** After the Hero paragraph type has been created, you can reuse its fields in other component's content types you will build later.
{% endhint %}

### Exercise: Creating a new paragraph type in Drupal

{% tabs %}
{% tab title="Hero Paragraph Type" %}
* From Drupal's Admin Toolbar, click **Structure \| Paragraph Types**
* Click the **Add paragraph type** button
* Assign the Label and Machine name below

  | Label | Machine name |
  | :--- | :--- |
  | Hero | `hero` |

* Click the **Save and manage fields** button

Add the following fields and settings to the paragraph type:

**NOTE:**: All fields use `1` as the **Allowed Number of values**.

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Title | `field_title` | Text \(Plain\) |
| Eyebrow | `field_eyebrow` | Text \(Plain\) |
| Body | `field_body` | Text \(Plain, long\) |
| Image | `field_image` | Media Reference |
| Call To Action | `field_cta` | Link |

For the Image field, set the following configuration:

* **Media type**: `image`

For the CTA field, set the following configuration:

* **Allowed link type**: _Both internal and external links_
* **Allowed link text**: _Required_
{% endtab %}

{% tab title="Quote Paragraph Type" %}


* From Drupal's Admin Toolbar, click **Structure \| Paragraph Types**
* Click the **Add paragraph type** button
* Assign the Label and Machine name below

  | Label | Machine name |
  | :--- | :--- |
  | Quote | `quote` |

* Click the **Save and manage fields** button

Add the following fields and settings to the paragraph type:

**NOTE:**: All fields use `1` as the **Allowed Number of values**.

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Title | `field_title` | Text \(Plain\) |
| Body | `field_body` | Text \(Plain, long\) |
| Image | `field_image` | Media Reference |
| Call To Action | `field_cta` | Link |
| Name | `field_name` | Text \(Plain\) |
| Job title | `field_job_title` | Text \(Plain\) |
| City | `field_city` | Text \(Plain\) |

For the Image field, set the following configuration:

* **Media type**: `image`

For the CTA field, set the following configuration:

* **Allowed link type**: _Both internal and external links_
* **Allowed link text**: _Required_
{% endtab %}
{% endtabs %}

### Putting the new paragraph type\(s\) to use

Now that the paragraph type is done, it's time to add it to a content type. Paragraph types on their own are useless. They need to be added to other entities such as a content type as an **Entity Reference** field.

### Adding the paragraph type to the Basic Page content type

* From Drupal's Admin Toolbar, click **Structure \| Content Types**
* Click the **Manage fields** button next to **Basic Page**
* Click the **Add field** button
* Under the _Add a new field_ dropdown, scroll to the **Reference Revisions** section and select **Paragraph**

  | Label | Machine name |
  | :--- | :--- |
  | Hero | `field_hero` |

* Click the **Save and continue** button
* Change _Allowed number of values\__ to **Limited - 1**
* In the _Reference Type_ section, choose **Hero** under _Paragraph type_
* Click the **Save settings** button

We'll use the Basic Page content type shortly to create a new Hero node.

