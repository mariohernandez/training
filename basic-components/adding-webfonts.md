# Adding webfonts

Pattern Lab:

{% tabs %}
{% tab title="_head.twig" %}
```markup
 <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Open+Sans:ital,wght@0,400;0,600;0,800;1,300;1,400&display=swap">
 <link rel="stylesheet" href="../../css/all.css?{{ cacheBuster }}" media="all" />
```
{% endtab %}
{% endtabs %}

Drupal Library:

{% tabs %}
{% tab title="storybook.libraries.yml" %}
```yaml
webfonts:
  css:
    base:
      'https://fonts.googleapis.com/css?family=Open+Sans:ital,wght@0,400;0,600;0,800;1,300;1,400&display=swap': { type: external, minified: true }
```
{% endtab %}
{% endtabs %}
