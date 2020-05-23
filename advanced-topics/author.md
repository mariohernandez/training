# Author

### Add new fields to the User profile  

1. From Drupal's admin toolbar, select **Configuration &gt; People &gt; Account Settings**
2. Click **Manage fields**
3. Click **Add field**
4. Add the following fields and their properties

| Label | Machine name | Field type | Allowed number of values |
| :--- | :--- | :--- | :--- |
| Full name | `field_full_name` | Text\(plain\) | 1 |
| Title | `field_title` | Text\(plain\) | 1 |

#### New User view mode

1. While still within the People Account Settings screen, click **Manage Display**
2. Under the **Default** view mode, expand the **CUSTOM DISPLAY SETTINGS** fieldset
3. Click **Manage view modes**
4. Scroll down to the **Users** section and click **Add new User view mode** link
5. Type **Custom** as the view mode name and click the **Save** button
6. Repeat steps 1 & 2 from _Add new fields to the User Profile ****_section at the top of the page
7. Expand the **CUSTOM DISPLAY SETTINGS** fieldset
8. Check **Custom** and click the **Save** button

#### Customize Custom view mode

1. From the list of view modes now available \(Default, Compact, and Custom\), click **Custom**
2. Drag the **Member for** field into the **Disabled** section
3. For the remaining fields, hide their labels by selecting **Hidden** in the Label's dropdowns
4. Click the **Save** button

#### Remove the link from the User's image

1. While still in the People Account Settings screen, click the gear icon to the right of the Image field
2. Change the **Link image to** dropdown to **Nothing**
3. Click the **Update** button
4. Click the **Save** button

