# Dependencies

After Drupal has been installed, let's add the following modules which we will use when interacting with Drupal

### Drupal modules

* [Components Libraries](https://www.drupal.org/project/components)
* [Devel](https://www.drupal.org/project/devel)
* [Admin toolbar](https://www.drupal.org/project/admin_toolbar)
* [Twig Field Value](https://www.drupal.org/project/twig_field_value)
* [Focal Point](https://www.drupal.org/project/focal_point)
* [Crop API](https://www.drupal.org/project/crop)
* Responsive Images (core)
* Media & Media Library (both on core)

### Download modules with composer

`ddev composer require drupal/components drupal/devel drupal/admin_toolbar drupal/twig_field_value drupal/focal_point drupal/crop`

### Enable modules

`ddev drush en components devel admin_toolbar admin_toolbar_tools twig_field_value focal_point crop`
