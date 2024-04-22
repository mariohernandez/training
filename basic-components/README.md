# Component Architecture

Grouping components or patterns in individual directories within your Drupal theme is a great practice when building components. This not only provides organization as your catalog of components grows, but it also makes components easier to share as all the pieces of a component are encapsulated in a single directory. Here's an example of a typical component architecture. Depending on the design system you use, your file types may vary.

```twig
|--src
|  |--components/
|     |--01-atoms/
|     |--02-molecules/
|        |--card
|           |-- card.css
|           |-- card.js
|           |-- card.twig
|           |-- card.yml
|           |-- card.stories.jsx
|     |--03-organisms/
```

A component is typically broken down as follows:

* **Markup** (required): Markup or HTML, is written in Twig, [Drupal's templating engine](https://www.drupal.org/docs/theming-drupal/twig-in-drupal)
* **Data** (optional): Demo or stock content for components is usually provided in YAML or JSON format. These are lightweight formats for storing data. In this training we will use [YAML](https://www.redhat.com/en/topics/automation/what-is-yaml){target=_blank rel=nooperner} to be more compatible with Drupal
* **Styles** (optional): These are typically written in CSS or a preprocessor like Sass
* **Interactions** (optional): The component's interactions are usually handled with JavaScript.  Most components don't need JavaScript
* **Story** (required): If using Storybook as your site's Styleguide or Design System, you will need a [*.stories.jsx](https://storybook.js.org/docs/get-started/whats-a-story){target=_blank rel=nooperner} file to convert the component to a format Storybook can understand.  Stories files typically use React code.
* **Documentation** (optional): Depending on your design system, this could be different type of files. For Storybook, a story's documentation is written in [MDX](https://storybook.js.org/docs/writing-docs/mdx){target=_blank rel=nooperner} format.
