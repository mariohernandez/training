# Author

Users in Drupal are another type of entity. This means we can theme them by using twig template suggestions. We'll start by adding a couple of fields that by default User profiles don't have. Then we will add a new view mode for users which will help us create the right template suggestion.

## Add new fields to the User profile

As we just saw in the Card Wide variant, we are displaying the article's author information. By default Drupal does not have a full name or title fields as part of user's profiles. Let's add these fields so we can use them in our cards.

1. From Drupal's admin toolbar, select **Configuration &gt; People &gt; Account Settings**
2. Click **Manage fields**
3. Click **Add field**
4. Add the following fields and their properties

| Label | Machine name | Field type | Allowed number of values |
| :--- | :--- | :--- | :--- |
| Full name | `field_full_name` | Text\(plain\) | 1 |
| Title | `field_title` | Text\(plain\) | 1 |

## New User view mode

We'll create a new view mode to control which user's fields we can display.

1. While still within the People Account Settings screen, click **Manage Display**
2. Under the **Default** view mode, expand the **CUSTOM DISPLAY SETTINGS** fieldset
3. Click **Manage view modes**
4. Scroll down to the **Users** section and click **Add new User view mode** link
5. Type **Author** as the view mode name and click the **Save** button
6. Repeat steps 1 & 2 from **Add new fields to the User Profile** section at the top of the page
7. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
8. Check **Author** and click the **Save** button

## Customize Author view mode

1. From the list of view modes now available \(Default, Author, and Compact\), click **Author**
2. Drag the **Member for** field into the **Disabled** section
3. For the remaining fields, hide their labels by selecting **Hidden** in the Label's dropdowns
4. Click the **Save** button

## Remove the link from the Author's image

1. While still in the People Account Settings screen, click the cogwheel icon to the right of the Image field
2. Change the view mode to **Medium \(220 x 220\)**
3. Change the **Link image to** dropdown to **Nothing**
4. Click the **Update** button
5. Click the **Save** button

## Update the Article content type to use the Author view mode

1. Go to Blog content type's manage display screen \(**Structure &gt; Content types &gt; Article &gt; Manage display**\)
2. Click the **Featured** view mode
3. For the Author field, ensure **Rendered entity** is set as the format
4. Click the little cogwheel icon to the right of the Author field
5. Change the view mode to **Author**
6. Click the **Update** then **Save** buttons

Changing the user's view mode to Author will help us create a new template suggestion for users.

