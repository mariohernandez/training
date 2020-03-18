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

