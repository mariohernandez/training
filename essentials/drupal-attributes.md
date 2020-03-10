# Drupal Attributes

In Drupal's twig templates you'll often see an attributes variable being output within the template. This variable is how core and contrib modules inject their CSS classes, an ID, or data attributes onto template markup. You'll also find title\_prefix and title\_suffix variables. These are used by core and contrib modules to inject markup into twig templates. A good example of this is the core Contextual Links module. If you were to remove the attributes, title\_prefix, and title\_suffix variables from a node template, for example, then the Contextual Links module would no longer have a way to add its drop-down to the display of nodes and this would make it impossible to inline edit the node or perform other tasks that are typically part of the Contextual Links module.

In some cases this may not be an issue for you, but in general it's best to plan to accommodate those Drupal-specific variables in your component markup so that when you integrate Drupal content into your components, other features can be available too. Since the attributes variable can include class, id, and data attributes in one variable, we need to make sure we only combine Drupal’s classes with ours, and let the other attributes render without Drupal classes. This can be accomplished on the main wrapper of the component template.

```php
<article class="card
  {{- attributes ? attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  {% if cover_image %}
    <div class="card__image">
      {{ image }}
    </div>
  {% endif %}
</article>
```

{% hint style="info" %}
Note that the `without` twig filter in this example is a Drupal-specific filter, so for the style guide we'll want to make sure we’re using one that supports Drupal’s custom filters. Pattern Lab has configuration options that support Drupal twig filters.
{% endhint %}

