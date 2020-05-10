# Building Drupal's back-end

### Enable the new theme

Enabling our new theme is not required to build Drupal's back-end for the Hero, but it's something we need to do at some point.  Let's do it now:

1. From Drupal's Admin Toolbar click **Appearance**
2. Scroll to the **Uninstalled themes** section where you will find the new theme you created.  It should have a thumbnail image with the Mediacurrent logo
3. Click **Install and set as default** under the theme name

### Disable CSS/JavaScript Aggregation

For some reason, Drupal core comes with CSS and Javascript Aggregation turned on out of the box.  Although this is highly recommended on production websites, during development it is recommended we turn aggregation off.  This will ensure CSS and Javascript code we write will be instantly available on our drupal pages without having to continuously clearn Drupal caches.

1. From Drupal's Admin toolbar click **Configuration &gt; Development &gt; Performance**
2. Clear bot check boxes: **Aggregate CSS files** & **Aggregate JavaScript files**
3. Click the **Save configuration** button
4. While you're at it, click the **Clear all caches** button on the same page

### Enable modules

Before we can build Drupal's back-end for the Hero and other components, we need to enable a few modules:

If you haven't already, enable the following modules:

* [Components Libraries](https://www.drupal.org/project/components)
* [Paragraphs](https://www.drupal.org/project/paragraphs) \(depends on [Entity Reference Revisions](https://www.drupal.org/project/entity_reference_revisions)\)
* [Devel & Kint](https://www.drupal.org/project/devel) \(both in same module\)
* [Admin toolbar](https://www.drupal.org/project/admin_toolbar) & Admin Toolbar Extra Tools
* [Twig Field Value](https://www.drupal.org/project/twig_field_value)
* [Focal Point](https://www.drupal.org/project/focal_point) \(depends on [Crop API](https://www.drupal.org/project/crop)\)
* Responsive Images \(core\)
* Media & Media Library \(both on core\)

### Drupal entities

Typically in a component-based project, Drupal will use entities to build the components infrastructure in the back end.  Entities such as content types, blocks, paragraph types, and even views, are some of the ways we can transition from a traditional development approach of building pages to a modular system of components.

Let's take the Hero component as an example, In Drupal we could build a custom block or a paragraph type called Hero.  This custom entity would be made of the same fields we identified when building the Hero component in Pattern Lab \(image, title, and CTA\). 

Let's build a Hero Paragraph type next.

