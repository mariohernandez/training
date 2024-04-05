# Dependencies

After Drupal has been installed, let's add or enable the following modules which we will use throughout this training.

## Core modules

* **Media**:
* **Responsive image**

## Contrib modules

* [Components Libraries](https://www.drupal.org/project/components)
* [Devel](https://www.drupal.org/project/devel)
* [Admin toolbar](https://www.drupal.org/project/admin_toolbar)
* [Twig Field Value](https://www.drupal.org/project/twig_field_value)
* [Twig tweak](https://www.drupal.org/project/twig_tweak)
* [Focal Point](https://www.drupal.org/project/focal_point)
* [Crop API](https://www.drupal.org/project/crop)
* Responsive Images (core)
* Media & Media Library (both on core)

## Download modules with composer

Navigate to the root of your drupal project and run the command below:

```php
ddev composer require 'drupal/components' 'drupal/devel' 'drupal/admin_toolbar' 'drupal/twig_field_value' 'drupal/twig_tweak' 'drupal/focal_point' 'drupal/crop
```

## Enable modules

```php
ddev drush en components devel admin_toolbar admin_toolbar_tools twig_field_value twig_tweak focal_point crop
```
