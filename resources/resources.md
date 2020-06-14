# Resources

## Fully functional D8 theme

* A fully functional Drupal 8 theme which includes all code in this training [can be downloaded from github](https://github.com/mariohernandez/training).
* [Google drive resources](https://drive.google.com/drive/folders/1oqwqIgEPP9V2qt_5lA5-mM6x9cEukHCj?usp=sharing)

## Drupal

* [Drupal Composer Project Templates ](https://www.drupal.org/docs/develop/using-composer/starting-a-site-using-drupal-composer-project-templates)
* [Drupal 8 Theming](https://www.drupal.org/docs/8/theming)
* [Drupal 8 Theming Guide](https://sqndr.github.io/d8-theming-guide/index.html)
* [Adding CSS and JavaScript to a Drupal 8 theme](https://www.drupal.org/docs/8/theming/adding-stylesheets-css-and-javascript-js-to-a-drupal-8-theme)
* [Drupal Behaviors](https://sqndr.github.io/d8-theming-guide/javascript/behaviors.html)
* [Drupal Attributes](https://www.drupal.org/docs/8/theming-drupal-8/using-attributes-in-templates)
* [Twig Field Value](https://www.drupal.org/project/twig_field_value) module
* [Twig Tweak](https://www.drupal.org/project/twig_tweak) module
* [Ensuring Drupal 8 Block Cache Tags bubble up to the Page](https://www.previousnext.com.au/blog/ensuring-drupal-8-block-cache-tags-bubble-up-page)
* [Render API](https://www.drupal.org/docs/8/api/render-api)
* [Setting Up Twig Debugging](https://www.chapterthree.com/blog/drupal-8-theming-setting-up-theme-debugging)
* [Limit Kint levels](https://gist.github.com/JPustkuchen/a5f1eaeb7058856b7ef087b028ffdfeb)

## Twig

* [Twig documentation](https://twig.symfony.com/doc/3.x/)
* [Twig for Template Designers](https://twig.symfony.com/doc/2.x/templates.html)
* [Twig blocks](https://twig.symfony.com/doc/2.x/tags/extends.html)
* [When to use Include, embed or extends](https://github.com/fourkitchens/emulsify/wiki/When-to-use-include,-extends,-and-embed)
* [Limit Kint levels when debugging](https://gist.github.com/JPustkuchen/a5f1eaeb7058856b7ef087b028ffdfeb)

## Blog Posts/Tutorials

* [Responsive Images](https://cloudfour.com/thinks/responsive-images-101-definitions/)
* [BEM 101](https://css-tricks.com/bem-101/)
* [Building and integrating drupal menus](https://www.mediacurrent.com/blog/building-and-integrating-menu-drupal/)
* [A walkthrough of the Theme Generator](https://www.youtube.com/watch?v=cVyA2v-UwSQ&feature=youtu.be)

## Screencasts/Video Tutorials

* [A Walkthrough of Mediacurrent's Theme Generator](https://www.youtube.com/watch?v=cVyA2v-UwSQ)

## Tools and Utilities

* [Mediacurrent Theme Generator](https://github.com/mediacurrent/theme_generator_8)
* [Pattern Lab](https://patternlab.io/)
* [Free stock image from Unsplash.com](https://unsplash.com/)
* [SMACSS](https://swapps.com/blog/what-is-smacss-and-how-to-use-it/)
* [Aspect ratio calculator](https://calculateaspectratio.com/)
* [Font sizing with REM](https://snook.ca/archives/html_and_css/font-size-with-rem)

## Snippets

### Create hook alter for user template suggestons

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

### Fixing 403 Forbidden error in Pattern Lab

* Create an `.htaccess` file in the root of your theme with the following code:  \(Some have reported the file should be inside the `patternlab` directory.  Try the theme's room first and recompile your theme\).

  ```php
  <FilesMatch "\.(twig)$">
  <IfModule mod_authz_core.c>
    Require all granted
  </IfModule>
  <IfModule !mod_authz_core.c>
    Order allow,deny
    Allow from all
  </IfModule>
  </FilesMatch>
  ```

