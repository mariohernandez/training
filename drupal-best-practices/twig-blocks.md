# Twig Blocks

## What are Twig Blocks?

Twig blocks are used for inheritance and act as placeholders and replacements at the same time. Twig blocks can be thought of as holes to fill in in a Drupal page.  Or perhaps as regions in your pages. Twig blocks are not the same, or have anything to do with Drupal blocks.

The challenge we face with Drupal theming is having control of the markup while adhering to Drupal's best practices for rendering content. When the time to integrate a component with Drupal comes, oftentimes using **include** statements will do the job, but there are times when we want to modify content or markup before Drupal renders a component and **include** statements don't allow for this. We could use the **extends** Twig statements but these could also be limiting. In these situations the best option is to use Twig's **embed** statements. Embed statements combine the functionality of both, **include** and **extends** statements. Let's see an example.

{% tabs %}
{% tab title="card.twig" %}

```php
<article class="card{{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  ...
  {% block extra_content %}
  {% endblock %}
</article>
```

{% endtab %}
{% endtabs %}

We've declared a twig block (`extra_content`), in which we can add or remove content. The block on its own does nothing. Currently we added the Twig block as a placeholder to use later.

Now let's make use of the twig block while we integrate the Card component with Drupal.

{% tabs %}
{% tab title="paragraph--card.html.twig" %}

```php

{% embed '@storybook/card/card.twig' with {
    title: title,
    image: content.field_image|render|trim is not empty ? content.field_image,
  }
%}
  {% block extra_content %}
    <h3>Hey this is new content</h3>
    <p>How cool is it that we can add or
    remove any content from here with twig blocks?</p>
  {% endblock %}
{% endembed %}
```

{% endtab %}
{% endtabs %}

The code above shows how we can add Twig blocks to any Twig template to add/remove content prior to rendering.
The example shows the following:

* When the Card component is integrated with a paragraph type of Card, we will add new content inside the twig block.
* We use a Twig **embed** statement to nest the Card component which allows us to alter the content inside the Twig block. This gives us a lot of flexibility and control to alter content before rendering. We will see other examples of Twig Blocks throughout this training.
