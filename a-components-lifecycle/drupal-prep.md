# Drupal prep

Before we can dive into building our component's infrastructure in Drupal, we need to get a few things ready. Perform each of the tasks below:

## Exercise: Enable the new theme

Enabling our new theme is not required to build Drupal's back-end for the Hero, but it's something we need to do at some point. Let's do it now:

1. From Drupal's Admin Toolbar click **Appearance**
2. Scroll to the **Uninstalled themes** section where you will find the new theme you created.  It should have a thumbnail image with the Mediacurrent logo
3. Click **Install and set as default** under the theme name

## Exercise: Disable CSS/JavaScript Aggregation

For some reason, Drupal core comes with CSS and Javascript Aggregation turned on out of the box. Although this is highly recommended on production websites, during development it is recommended we turn aggregation off. This will ensure CSS and Javascript code we write will be instantly available on our drupal pages without having to continuously clearn Drupal caches.

1. From Drupal's Admin toolbar click **Configuration > Development > Performance**
2. Clear both check boxes: **Aggregate CSS files** & **Aggregate JavaScript files**
3. Click the **Save configuration** button
4. While you're at it, click the **Clear all caches** button on the same page

## Exercise: Enable modules

If you haven't already, enable the following modules:

* [Components Libraries](https://www.drupal.org/project/components)
* [Paragraphs](https://www.drupal.org/project/paragraphs) (depends on [Entity Reference Revisions](https://www.drupal.org/project/entity_reference_revisions))
* [Devel](https://www.drupal.org/project/devel)
* [Admin toolbar](https://www.drupal.org/project/admin_toolbar) & Admin Toolbar Extra Tools
* [Twig Field Value](https://www.drupal.org/project/twig_field_value)
* [Focal Point](https://www.drupal.org/project/focal_point) (depends on [Crop API](https://www.drupal.org/project/crop))
* [Views Reference Field](https://www.drupal.org/project/viewsreference)
* Responsive Images (core)
* Media & Media Library (both on core)
