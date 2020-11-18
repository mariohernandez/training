# Component Architecture

I typically recommend to group components or patterns in individual folders within your Drupal theme. This not only provides organization as your catalog of components grows, but it also makes each component completely reusable and even portable as all the pieces of a component are encapsulated in a single folder. Here's an example of a typical component architecture. Your particular workflow may vary.

```text
+
|--src
|  |--patterns
|     |--components
|        |--card
|           |-- card.js
|           |-- card.md
|           |-- card.scss
|           |-- card.twig
|           |-- card.json
+
```

A component is typically broken down in four parts:

* **Markup**: Markup or HTML for a component is written in [Twig templates, Drupal 8's templating engine](https://www.drupal.org/docs/theming-drupal/twig-in-drupal). 
* **Data**: Dummy or stock data for components is usually provided in YAML or JSON format. These are lightweight formats for storing data. In this training we will use JSON \(**J**ava**S**cript **O**bject **N**otation\).
* **Styles**: These are written in CSS or SCSS.
* **Behavior/interaction**: The component's behaviors are usually handled with JavaScript.  Most components don't need JavaScript.
* **Annotations** \(Optional\): Annotations are used to document the details of a component and are typically written in markdown format \(`.md`\). This is extremely useful for teams because it outlines technical details of a pattern such as variable names, attributes, data structure, etc.

