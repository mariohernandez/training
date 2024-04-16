# Drupal Attributes

In Drupal you'll often see an attributes variable being output in twig templates. This variable is how core and contrib modules inject their CSS classes, IDs, or data attributes onto template markup. You'll also find `title_prefix` and `title_suffix` variables. These are used by core and contrib modules to inject markup into twig templates. A good example of this is the core Contextual Links module. If you were to remove the attributes, title\_prefix, and title\_suffix variables from a node template, for example, then the Contextual Links module would no longer have a way to add its drop-down to the display of nodes and this would make it impossible to inline edit the node or perform other tasks that are typically part of the Contextual Links module.

In some cases this may not be an issue for you, but in general it's best to plan to accommodate those Drupal-specific variables in your component markup so that when you integrate Drupal content into your components, other features can be available too. Since the attributes variable can include class, id, and data attributes in one variable, we need to make sure we only combine Drupal’s classes with ours, and let the other attributes render without Drupal classes. This can be accomplished in different ways, but my personal approach is by adding these variables on the main wrapper of the component template like this:

```php
<article class="card{{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  {% if cover_image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}
</article>
```

{% hint style="info" %}
Note that the `without` twig filter in this example is a Drupal-specific filter, so for the style guide we'll want to make sure we’re using one that supports Drupal’s custom filters. Pattern Lab has configuration options that support Drupal twig filters.
{% endhint %}
