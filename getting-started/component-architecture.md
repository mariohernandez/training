# Component Architecture

Components are typically saved in a project's theme and although they will work regardless of where in your theme they are stored, it is recommended to group them in folders. This not only provides organization as your catalog of components grows, but it also makes each component completely reusable and even portable as all the pieces of a component are encapsulated in a single folder. Here's a typical architecture of a component. Your particular workflow may vary.

```text
+
|--src
|  |--patterns
|     |--components
|        |--quote
|           |-- quote.js
|           |-- quote.md
|           |-- quote.scss
|           |-- quote.twig
|           |-- quote.yml or .json
+
```

A component is typically broken down in four parts:

* **Markup**: Markup or HTML for a component is written in Twig templates, Drupal's new templating engine. Naming convention for a component twig template looks like this: quote.twig \(where quote is the name of the component\).
* **Data**: For the purpose of the style-guide, we need dummy or stock data, which is normally provided in YAML or JSON format.
* **Styles**: These are written in CSS or SCSS.
* **Behavior/interaction**: The component's behaviors are usually handled with JavaScript.
* **Annotations** \(Optional\): Annotations are used to document the details of a component and are typically written in markdown format. This is extremely useful for developers because it outlines technical details of a pattern such as variable names, attributes, data structure, etc.

{% hint style="info" %}
Not every component will need a javascript file.
{% endhint %}

