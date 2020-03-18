# Paragraph Types

## Hero

There are many ways to build the hero in Drupal.  To keep things simple we will use a paragraph type in which we will add all the fields we identified when building the Hero component in Pattern Lab.

Using the table below, create a new paragraph type called **Hero**.

| Label | Machine name |
| :--- | :--- |
| Hero | `hero` |

Add the following fields and settings to the paragraph type:

| Field label | Machine name | Field type |
| :--- | :--- | :--- |
| Title | `field_title` | Text \(Plain\) |
| Eyebrow | `field_eyebrow` | Views Reference |
| Body | `field_body` | Views Reference |
| Image | `field_image` | Views Reference |
| Button | `field_button` | Views Reference |

For the Movie list view field, set the following configuration:

| Type to reference | Default Value | View Display | Preselect view option |
| :--- | :--- | :--- | :--- |
| View | Movie List view, List via Term ID | Block | Movie list |

