# Card paragraph type

Follow the stepsbelow to build a paragraph type for the Card component.

{% hint style="info" %}
**TIP:** You can reuse fields from previously created entities such as Hero paragraph type.
{% endhint %}

{% tabs %}
{% tab title="Card Paragraph Type" %}
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
{% endtab %}
{% endtabs %}

