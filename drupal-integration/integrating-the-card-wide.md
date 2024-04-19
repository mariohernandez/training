# Integrating the Card Wide

![Card Wide variant](../.gitbook/assets/card-wide.png)

In the previous exercise we used the default card component to display blog posts that are part of the **From our blog** section. In this exercise, you will use the **Card Wide** variant to style blog posts that are part of the **Featured Content** section. The process for achieving this is exactly as we did with the regular card in the previous exercise. Here are some things to note:

* In the previous exercise we used the **Teaser** view mode to create a custom twig template.  In this exercise use the **Featured** view mode
* In order to achieve the Card Wide look, we need to pass a modifier class of `card--wide` when the component is integrated
* The card wide does not use `tags`, but it does use the `author` field
* Use the appropriate twig block for displaying the date, in **short** format.  Remember, we created two twig blocks in the card component to determine where the date will be displayed depending on the card we are working with.
* Finally, the template suggestion you will need to create is `node--article--featured.html.twig`

## Full integration code

Here is what **node--article--featured.html.twig** looks like when the Card Wide is integrated.

{% tabs %}
{% tab title="node--blog--featured.html.twig" %}
```php
{# Sets variable to trigger content render array. #}
{% set rendered_content = content|render %}

{#
Sets variable for article title to provide all
properties needed by the heading component (heading_level,
modifier, title, and url).
#}
{% set article_title = {
    "heading_level": 3,
    "modifier": "card__title",
    "title": label,
    "url": url
  }
%}

{#
Uses embed to be able to include card component
and make use of twig blocks found in such component.
#}
{% embed '@components_theme/card/card.twig' with
  {
    "attributes": attributes,
    "title_prefix": title_prefix,
    "title_suffix": title_suffix,
    "image": content.field_image is not empty ? content.field_image,
    "heading": article_title,
    "date": node.createdtime|date('M d'),
    "category": content.field_category|render|trim is not empty ? content.field_category,
    "body_text": content.body|render|trim is not empty ? content.body,
    "author": content.field_author,
    "modifier": 'card--wide'
  } only
%}

  {# Calls featured_date twig block.#}
  {% block featured_date %}
    {{ date }}
  {% endblock featured_date %}

  {#
  Removes content from card_date twig block
  to avoid printing the date twice and in
  different places.
  #}
  {% block card_date %}
  {% endblock card_date %}

  {# Calls author twig block.#}
  {% block author %}
    {{ author }}
  {% endblock author %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

* Save the changes above and clear Drupal's cache
* Reload Drupal's homepage
*  The Featured Content section rendered with the Card wide.  But there seems to be a problem with the author information.  Let's fix it next
