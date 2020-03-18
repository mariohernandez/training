# Paragraph Types

## Hero

There are many ways to build the Hero in Drupal.  One very common approach is to use a paragraph type. Using a paragraph type will allow us to reuse the hero on any page we need to.

Using the table below, create a new paragraph type called **Hero**
* From Drupal's Admin Toolbar, click **Structure | Paragraph Types**
* Click the **Add paragraph type** button

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