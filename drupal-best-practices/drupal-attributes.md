# Drupal attributes

In Drupal you'll often see an attributes variable being output in twig templates. This variable is how core and contrib modules inject their CSS classes, IDs, or data attributes onto template markup. You'll also find `title_prefix` and `title_suffix` variables. These are used by core and contrib modules to inject markup into twig templates. A good example of this is the core Contextual Links module. If you were to remove the attributes, `title_prefix`, and `title_suffix` variables from a node template, for example, then the Contextual Links module would no longer have a way to add its drop-down to the display of nodes and this would make it impossible to inline edit the node or perform other tasks that are typically part of the Contextual Links module.

In some cases this may not be an issue for you, but in general it's best to plan to accommodate those Drupal-specific variables in your component markup so that when you integrate Drupal content into your components, other features can be available too. Since the attributes variable can include class, id, and data attributes in one variable, we need to make sure we only combine Drupal’s classes with ours, and let the other attributes render without Drupal classes. This can be accomplished in different ways, but my personal approach is by adding these variables on the main wrapper of the component template like this:

```php
<article class="card{{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  {{ title_suffix }}
  {% if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}
</article>
```

So we are adding placeholders for attributes in two ways: The first is we are grouping Drupal's classes (`attributes.class`) with any custom classes we are adding to the component (i.e. `card`), then, we place the attributes object a second time but this time without classes, meaning we will only get IDs or data attributes Drupal may provide.
