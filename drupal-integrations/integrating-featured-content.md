# Integrating Featured Content

Now let's repeat what we just did with the From our blog section, with the Featured Content.

In this case we will only create one view template suggestion, only for the Featured content block `views-view--blog-posts--featured-content.html.twig`.  Since both blocks \(**from-our-blog** & **featured-content**\), are part of the same view \(Blog posts\), and they both use the same data format of `unformatted` , we can use the same template for both blocks.  This means `views-view--unformatted--blog-posts.html.twig` will serve both sections of content.

1. Make a copy of `views-view.html.twig` and name it `views-view--blog-posts--featured-content.html.twig`
2. Add the following code overriding all existing code in the template.  Don't delete the comments.

{% tabs %}
{% tab title="view-view--blog-posts--featured-content.html.twig" %}
```php
{%
  set classes = [
    dom_id ? 'js-view-dom-id-' ~ dom_id,
  ]
%}

{% set attributes = attributes.addClass(classes) %}

{# Variable for the view title #}
{% set heading = {
    "heading_level": '2',
    "modifier": 'heading--large center section-header',
    "title": 'Featured content',
    "url": ''
  }
%}

{% embed '@training_theme/featured-content/featured-content.twig' %}
  {% block featured_items %}
    {{ rows }}
  {% endblock %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

* Just like we did for the From our blog integration, we are leaving the `dom_id` class available and adding it to the template's attributes.
* Also as we did before, we are setting a new variable for the `heading` or section title.
* Finally we are embedding the `featured-content.twig` component and printing its content inside a twig block called `featured_items`.
* Save your changes and clear Drupal's cache.
* Reload the homepage and you should see the **Featured content** section nicely styled.



