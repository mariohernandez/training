# Hero Component

We are now finally at a point where we can integrate the Hero component using the Hero paragraph type in Drupal.

1. Open `/src/templates/paragraphs/paragraph--hero.html.twig` in your text editor
2. Remove all code in the file but leave all comments. It is good to leave the comments untouched as they provide helpful information regarding available variables and other useful Drupal-specific details.
3. Add the following code at the bottom of the template:

```php
{% set rendered_content = content|render %}

{%
  include '@theme_name/hero/hero.twig' with {
    attributes: attributes,
    title_prefix: title_prefix,
    title_suffix: title_suffix,
    image: content.field_image|render|trim is not empty ? content.field_image,
    eyebrow: content.field_eyebrow|render|trim is not empty ? content.field_eyebrow,
    heading: {
      title: content.field_title|render|trim is not empty ? content.field_title
    },
    body: content.field_body|render|trim is not empty ? content.field_body,
  } only
%}
```

Let's go over what we are doing here:

* First, as mentioned in [Drupal Best Practices](https://mariohernandez.gitbook.io/training/essentials/drupal-best-practices#passing-fields-values-to-components), we're triggering a full render of the content array variable.
* Next, we are setting up a variable that will include the values for the **heading** of the movie card that are based on variables Drupal provides. If you notice starting around line 18 in the comments of our template file, the _label_ variable is the Node's title, and the _url_ variable is the node's URL. In addition, notice that the _heading_ variable we created is modeled after the _**heading**_ component's [YAML object](https://mariohernandez.gitbook.io/components/~/drafts/-L_4qJ97wL1R7eH6ZDkg/primary/chapter-4/building-components/2-heading#improving-the-heading-component).
* Next we use an `embed` twig statement to integrate the Movie card component. In the embed we are mapping all the Movie card fields with Drupal's data. We also pass in Drupal-specific items such as _title\_prefix_, _title\_suffix_, _attributes_, etc.
* Notice how with the average viewer rating field we are making use of the `field_value` filter that's provided by the [Twig Field Value](https://www.drupal.org/project/twig_field_value) module to pass in the raw value of that field. This is because in our template for the Average Viewer Rating component we're expecting a simple number for a data attribute, so if it were to include any markup it would break our component!
* Finally we make use of the `favorites_toggle` twig block tag that we set up in the movie card component to swap out what is output in that area of the component. We're instead letting Drupal render the flag field as provided by the flag module. It's like we're telling Drupal "Use **our** component with your field values, except for the add-to-favorites button -- take care of that one for us, would ya?"

add this somewhere for info on [how to check for empty fields](https://www.drupal.org/project/drupal/issues/2547559)

### 

#### 

