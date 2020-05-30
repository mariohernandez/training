# Hook alter

This hook alter allows for creating template suggestions for users.
Add this hook alter to your theme's `training_theme.theme` file.

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
