# Date formats

We are using the date in two different ways.  In the regular card we are using a long format and in the card wide we are using a short format.  We are going to create these two formats using Drupal's out of the box date formats.

1. In Drupal, click on **Configuration &gt; Regional and language &gt; Date and time formats**
2. Click **Edit** next to **Default long date**
3. In the **Format string** field, update its value with `l, F j, Y`
4. Click **Save format**
5. Repeat these steps with **Default short date** and replace its value with `F j`
6. Save your changes.

{% hint style="info" %}
Drupal uses PHP date formats.  [Learn more ](https://www.php.net/manual/en/function.date.php)about these formats.
{% endhint %}

### Update the date format in the teaser template

Now that we've updated Drupal's date formats, let's make use of one of them. We will use the other one when we integrate the card wide components.

1. Add the following code in `node--blog--teaser.html.twig` \(above all previous code\)

{% tabs %}
{% tab title="node--blog--teaser.html.twig" %}
```php
{% set date = node.createdtime|format_date('long') %}
```
{% endtab %}
{% endtabs %}

* We are setting a variable for date to change its format to the **long** format we just setup.

### Full integration code

Now the full integration template should look like below. Clear Drupal's cache again and reload the homepage. The date format on the articles using the card should now match our designs.

{% tabs %}
{% tab title="node--blog--teaser.html.twig" %}
```php
{# Sets date variable to change to short format. #}
{% set date = node.createdtime|format_date('long') %}

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
{% embed '@training_theme/card/card.twig' with
  {
    "attributes": attributes,
    "title_prefix": title_prefix,
    "title_suffix": title_suffix,
    "title": article_title,
    "image": content.field_blog_image|render|trim is not empty ? content.field_blog_image,
    "date": date,
    "body_text": content.body|render|trim is not empty ? content.body,
    "tags": content.field_blog_tags|render|trim is not empty ? content.field_blog_tags,
    "modifier": ""
  } only
%}

  {#
  Removes content from featured_date twig block
  to avoid printing the date twice and in
  different places.
  #}
  {% block featured_date %}
  {% endblock featured_date %}

  {# Calls card_date twig block. #}
  {% block card_date %}
    {{ date }}
  {% endblock card_date %}

  {# Outputs tags. #}
  {% block tags %}
    {{ tags }}
  {% endblock tags %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

If you save your changes and reload Drupal's homepage \(you may need to clear caches\), you will see the date now shows in the right format.  Now let's fix the tags issues.

