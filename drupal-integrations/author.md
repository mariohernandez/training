# Author integration

Out of the box Drupal does not provide template suggestions for users. After researching a little I found a hook alter that will allow us to create new template suggestions.

1. In your editor, open `training_theme.theme` which is located in the root of your theme
2. Add the following code:

{% tabs %}
{% tab title="training\_theme.theme" %}
```php
/**
 * Implements hook_theme_suggestions_user_alter().
 *
 *   An array of alternate, more specific names for template files or theme
 *   functions for users.
 */
function training_theme_theme_suggestions_user_alter(&$suggestions, $vars, $hook) {

  // Define the view mode.
  $mode = $vars['elements']['#view_mode'];

  // Create a theme hook suggestion which has the view mode name in it.
  $suggestions[] = 'user__' . $mode;
}
```
{% endtab %}
{% endtabs %}

* The hook alter above will make it possible for Drupal to provide some useful twig template suggestions.
* Clear Drupal's cache
* Inspect the user by right-clicking over the user's picture and selecting **Inspect** or **Inspect Element**
* As you scroll through the debugging info in your inspector you should be able to see template suggestions for users.  See screenshot:

![User template suggestions](../.gitbook/assets/user.png)

* By default Drupal uses `user.html.twig` to render all users. Thanks to the hook alter we added earlier we now see a new template suggestion, `user--author.html.twig`. This template is using the new view mode we created for our users earlier.
* Copy `user.html.twig` from the path shown in the image above \(`core/themes/stable/templates/user/`, into your theme's `/templates/user` folder
* Rename the newly copied template `user--author.html.twig`
* Clear Drupal's cache
* If you reload the homepage again and inspect the user you should see our new template suggestion being used by Drupal.

## Integrating the Author component

1. Open `user--author.html.twig` in your editor and as we've done with all template suggestions, delete all the code except the comments
2. Add the following code and save the file

{% tabs %}
{% tab title="user--author.html.twig" %}
```php
{% include "@training_theme/author/author.twig" with
  {
    "attributes": attributes,
    "author": {
      "photo": content.user_picture,
      "name": content.field_full_name,
      "title": content.field_title
    }
  }
%}
```
{% endtab %}
{% endtabs %}

* Reload Drupal's homepage and you should now see the author information properly themed.

