# Drupal best practices

## Presenter templates

Presenter templates are Twig template suggestions in a theme (e.g., `node--news.html.twig`, `block--card.html.twig`, `field--something.html.twig`, etc.), but in the context of Component-driven development, their only purpose is to pass data from Drupal to the components. This means Markup, CSS and Javascript is all handled in Storybook and not in presenter templates.

Presenter templates are probably the most popular way to integrate front-end components with Drupal, but there are also other ways such as the [UI Patterns](https://www.drupal.org/project/ui_patterns){target=_blank rel=nooperner} module and pre-process functions.

## Presenter templates best practices

* It’s best to try and loyally follow the atomic design approach as much as possible when creating components.
* When at the molecule/organism level of your components, use twig **blocks** (not the same or related to Drupal blocks), generously to help with future embeds of those components.  If in doubt, block it out.
* Let Drupal render all fields at the theme level with little to no pre-processing and use view modes as much as possible.
* Use modules that extend twig ([twig field value](https://www.drupal.org/project/twig_field_value), [twig tweak](https://www.drupal.org/project/twig_tweak), etc.) when only the field value is required.
* Create twig templates to help remove bloated field markup, and make use of twig’s extends statements to help streamline reusability and reduce duiplicate code.
* Accommodate Drupal’s attributes object and title_prefix/suffix variables when that’s necessary.

## Benefits of this approach

* It’s (mostly) twig, css, js, with no PHP.
* Although you may end up with more twig template files, you can set up a directory structure that helps keep them logically organized, and easier to see how things piece together.
* It is more straightforward when it comes to accommodating Drupal’s methods for injecting features from contrib modules (i.e., attributes object).

## Passing fields values to components

With the presenter template method you'll quickly discover that when passing the value of a field to your component, Drupal does not give us the raw value of that field, we're instead given a [render array](https://www.drupal.org/docs/8/api/render-api/render-arrays), and when that array is rendered, it includes a lot of default markup that will often get in the way of theming. While we may be tempted to just pluck the value that we want from the render array and pass it to our component, it's best to try and let Drupal fully render the field to avoid cache invalidation issues. We will see examples of this as we build components.
