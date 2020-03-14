# Before the Integration

Before we beging integrating components with Drupal, there are some preparation to be done and some practices to understand.

### What is component integration?

At a high level, component integration means wiring Drupal Twig templates to pre-built components from a design system such as Pattern Lab.  By default Drupal has no knowledge of any components in Pattern Lab, but with the [Component Libraries](https://www.drupal.org/project/components) module and through the use of Presenter templates, we make Drupal aware of components so they get rendered using Drupal data while keeping Pattern Lab as the single source of truth for the component's markup, styles and javascript.

### Twig debugging

Twig debugging is not required for integrating components but it is highly recommended as this will make your job easier.  Enabling Twig debugging will allow us to identify the right Drupal templates we need to work with to integrate components.  These templates are typically know as template suggestion.  More on this shortly.

&lt;add instructions to enable twig debugging&gt;

### Drupal entities

Typically in a component-based project, Drupal will use entities to build the components infrastructure in the back end.  Entities such as nodes, blocks, paragraph types, and even views, are some of the ways we can transition from a traditional development approach of building pages to a modular system of components.

Let's take the Hero component as an example, In Drupal we could build a custom block or a paragraph type called Hero.  This custom entity would be made of the same fields we identified when building the Hero component \(image, eyebrow, title, body, cta\). 

