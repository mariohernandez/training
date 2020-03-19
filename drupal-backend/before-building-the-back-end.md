# Before building the back-end

Before we can build Drupal's back-end for the Hero and other components, do the following:

If you haven't already, enable the following modules:

* [Components Libraries](https://www.drupal.org/project/components)
* [Paragraphs](https://www.drupal.org/project/paragraphs)
* [Devel & Kint](https://www.drupal.org/project/devel) \(both in same module\)
* [Admin toolbar](https://www.drupal.org/project/admin_toolbar)
* [Twig Field Value](https://www.drupal.org/project/twig_field_value)
* [Focal Point](https://www.drupal.org/project/focal_point)
* Responsive Images \(core\)
* Media & Media Library \(both on core\)

### Drupal entities

Typically in a component-based project, Drupal will use entities to build the components infrastructure in the back end.  Entities such as nodes, blocks, paragraph types, and even views, are some of the ways we can transition from a traditional development approach of building pages to a modular system of components.

Let's take the Hero component as an example, In Drupal we could build a custom block or a paragraph type called Hero.  This custom entity would be made of the same fields we identified when building the Hero component in Pattern Lab \(image, eyebrow, title, body, cta\). 

