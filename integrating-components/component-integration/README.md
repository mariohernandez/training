# Before the Integration

Before we beging integrating components with Drupal, there are some preparation to be done and some practices to understand.

### What is component integration?

At a high level, component integration means wiring Drupal Twig templates to pre-built components from a design system such as Pattern Lab.  By default Drupal has no knowledge of any components in Pattern Lab, but with the [Component Libraries](https://www.drupal.org/project/components) module and through the use of Presenter templates, we make Drupal aware of components so they get rendered using Drupal data while keeping Pattern Lab as the single source of truth for the component's markup, styles and javascript.

### Disable Drupal Caching and enable Twig debugging

Twig debugging is not required for integrating components but it is highly recommended as this will make your job easier.  Disabling caching Enabling Twig debugging during development will allow us to identify the right Drupal templates we need to work with to integrate components.  These templates are typically know as template suggestion.  More on this shortly.

{% hint style="info" %}
**DO THIS:**  [Follow these instructions](https://www.drupal.org/node/2598914) to disable Drupal caching and enable debugging during development.  Depending on your environment, these instructions may vary.
{% endhint %}

