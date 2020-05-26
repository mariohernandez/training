# Hook alter for container

Sometimes Drupal adds markup that gets in the way of rendering page elements properly.  It only takes an extra `<div>` to break the layout or styles of a component.  For this reason, I was forced to create hook alter to remove all markup wrappers in templates used by the Featured Content and From our blog.

```php
/**
 * Implements hook_theme_suggestions_container_alter().
 */
function training_theme_theme_suggestions_container_alter(&$suggestions, array $variables) {
  $element = $variables['element'];

  if (isset($element['#type']) && $element['#type'] == 'view') {
    $suggestions[] = 'container__' . $element['#name'];
    $suggestions[] = 'container__' . $element['#name'] . '__' . $element['#display_id'];
  }

  if (isset($element['#type']) && $element['#type'] == 'container' && isset($element['children']['#type'])) {
    $suggestions[] = 'container__' . $element['children']['#type'];
  }
}
```
