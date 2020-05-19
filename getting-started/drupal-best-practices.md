# Drupal Best Practices

## Presenter templates

Presenter templates are Twig templates in a theme \(e.g., `node.html.twig`, `block.html.twig`, `field.html.twig`, etc.\), but in the context of Component-development, their only purpose is to pass data from Drupal to the component. This means everything related to the component such as Markup, CSS and Javascript is done at the component level in Pattern Lab, and when it’s time to wire the component with Drupal, we use the appropriate presenter template, or Twig template suggestion, to simply map the Drupal fields with the component's fields we defined in Pattern Lab.

There are other ways to integrate component with Drupal, such as the [UI Patterns](https://www.drupal.org/project/ui_patterns) module, pre-processing, but the most popular approach is presenter templates.

## Presenter templates best practices

* It’s best to try and loyally follow the atomic design approach as much as possible when creating components.
* When at the molecule/organism level of your components, use twig **block tags** generously to help with future embeds of those components.  If in doubt, block it out.
* Let Drupal render all fields at the theme level with little to no pre-processing. Use view modes as much as possible.
* Use modules that extend twig \([twig field value](https://www.drupal.org/project/twig_field_value), [twig tweak](https://www.drupal.org/project/twig_tweak), etc.\) when only the field value is required.
* Create twig template files to help remove bloated field markup, and make use of twig’s extends statements to help streamline reuse of field templates.
* Accommodate Drupal’s attributes object and title\_prefix/suffix variables when that’s necessary.

## Benefits of this approach

* It’s \(mostly\) twig, scss/css, js, with no PHP.
* Although you may end up with lots of twig template files, you can set up a directory structure that \(hopefully\) helps keep them logically organized, and easier to see how things piece together.
* It should be more straightforward when it comes to accommodating Drupal’s methods for injecting features from contrib modules \(i.e., attributes object\).

## Passing fields values to components

In the presenter template method you'll quickly discover that when passing the value of a field to your component, Drupal does not give us the raw value of that field, we're instead given a [render array](https://www.drupal.org/docs/8/api/render-api/render-arrays), and when that array is rendered, it includes a lot of default markup that will often get in the way. While we may be tempted to just pluck the value that we want from the render array and pass it to our component, it's best to try and let Drupal fully render the field to avoid cache invalidation issues. We will see examples of this as we build components.

