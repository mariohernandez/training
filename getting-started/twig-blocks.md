# Twig Blocks

The challenge we face is having control of the markup while adhering to Drupal's best practices for rendering content. When the time to integrate a component with Drupal comes, often times using `include` statements will do the job, but there are times when we want to modify content or markup before Drupal renders a component and `include` statements don't allow for this. We could use the `extends` Twig statements but these could also be limiting. In these situations the best option is to use Twig's `embed` statements.  Embed statements combine the functionality of both, `include` and `extend` statements. Let's see an example.

```php
<article class="card
  {{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  ...
  {% block card_extra_content %}
  {% endblock %}
</article>
```

We've declared a twig block \(`card_extra_content`\), in which we can add or remove any content we want. The block on its own does nothing. Currently we added the Twig block as a placeholder to use later.

{% hint style="warning" %}
**IMPORTANT:** Twig blocks are not the same, and have nothing to do with Drupal blocks.
{% endhint %}

```php
{% embed '@patterns/card/card.twig' with {
    heading: heading,
    image: content.field_image|render|trim is not empty ? content.field_image,
  }
%}
  {% block card_extra_content %}
    <h3>Hey this is new content</h3>
    <p>How cool is it that we can add or
    remove any content from here with twig blocks?</p>
  {% endblock %}
{% endembed %}
```

The code above shows how we can use the Card component somewhere and we can make use of the Twig Block, in this example by adding new content the card component did not originally provide.  This gives us a lot of flexibility and control to alter content before rendering.  We will see other examples of Twig Blocks  throughout this training.

