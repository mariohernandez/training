# Taxonomy terms

Taxonomy are Drupal entities just like Nodes, blocks, etc. This means we can create view modes and custom templates so we can integrate them with Drupal. Currently we don't have a component for displaying tags. Having a dedicated component for tags will allow us to individually style them and will allow for more effective integration with Drupal. Let's quickly build one.

## Build a component for the tags

The tags component is going to be a little unusual compared to other components we've built. The main reason for the way this component will be built is how Drupal handles templates for taxonomy terms and vocabularies. We will see more about this when we integrate the tag components with Drupal.

1. Inside `src/patterns/components/` create a new folder called **tags**
2. Inside the _tags_ folder create a new file called `tag-item.twig` (_we will first create a component for a single tag item_).  
   1. Since we wouldn't want to display only a single tag item in Pattern Lab, let's hide it by creating a new file called **tag-item.md**\
      Inside the markdown file add the following code:\
      `---`\
      `hidden: true`\
      `---`
   2. Using a markdown file with the same name of the pattern you wish to hide will hide the pattern in Pattern Lab.  The pattern is still available if we need to use it in another component. 
3. Add the following code inside `tag-item.twig`

{% tabs %}
{% tab title="tag-item.twig" %}
```php
<span{% if attributes %} class="{{ attributes.class }}"{% endif %}
  {{- attributes ? attributes|without(class) -}}>
  {{ title_prefix }}
  <a href="{{ url }}" class="tag__link">
    {{ name }}
  </a>
  {{ title_suffix }}
</span>
```
{% endtab %}
{% endtabs %}

1. Now inside the _tags_ folder create the following files with the following code:

{% tabs %}
{% tab title="tags.json" %}
```yaml
{
  "items": [
    {
      "name": "Frashion",
      "url": "#"
    },
    {
      "name": "Sports",
      "url": "#"
    },
    {
      "name": "Health",
      "url": "#"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="tags.twig" %}
```php
{{ attach_library('training_theme/tags') }}

<ul class="tags{{ modifier ? ' ' ~ modifier }}
  {{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>
  {% for item in items %}
    <li class="tag__item">
      {% block tag_item %}
        {%
          include '@training_theme/tags/tag-item.twig' with {
            "name": item.name,
            "url": item.url
          } only
        %}
      {% endblock %}
    </li>
  {% endfor %}
</ul>
```
{% endtab %}
{% endtabs %}

* Notice we are including the single tag item while we look through the items array.

{% tabs %}
{% tab title="tags.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.tags {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.tag__item {
  align-items: center;
  border-radius: 2px;
  color: $color-gray-dark;
  display: flex;
  justify-content: center;
  line-height: 1;
  margin-right: 10px;


  a {
    background-color: $color-black;
    color: $color-white;
    display: block;
    font-size: 1.3rem;
    line-height: 1.2;
    padding: 6px 12px;
    text-decoration: none;
    transition: background-color 0.2s ease;

    &:hover,
    &:focus {
      background-color: lighten($color-black, 15%);
    }
  }
}
```
{% endtab %}
{% endtabs %}

* If you save your changes and compile your code you should see a list of tags in Pattern Lab.  Let's integrate this component with Drupal now to fix our tags inside the card of blog posts.

{% hint style="info" %}
Don't forget to create the Drupal library for the tags.
{% endhint %}

## Updated the card

Now that we have a component for tags, let's modify the card so we make use of it. Here's the full card.twig code which now uses an include for the tags.

{% tabs %}
{% tab title="card.twig" %}
```php
{{ attach_library('training_theme/card') }}

<article class="card{{ modifier ? ' ' ~ modifier }}
  {{- attributes ? ' ' ~ attributes.class -}}"
  {{- attributes ? attributes|without(class) -}}>

  {# Date for featured content cards. #}
  {% if 'card--wide' in modifier %}
    <div class="card__featured--date">
      {% block featured_date %}
        {{ date }}
      {% endblock featured_date %}
    </div>
  {% endif %}

  {% if image %}
    <div class="card__media">
      {{ image }}
    </div>
  {% endif %}

  <div class="card__content">
    {% if heading %}
      {{ title_prefix }}
      {%
        include '@training_theme/heading/heading.twig' with {
          heading: heading
        } only
      %}
      {{ title_suffix }}
    {% endif %}

    {# Date for regular content cards. #}
    {% if 'card--wide' not in modifier %}
      <div class="eyebrow card__date">
        {% block card_date %}
          {{ date }}
        {% endblock card_date %}
      </div>
    {% endif %}

    {% if category %}
      <div class="eyebrow card__category">
        {{ category }}
      </div>
    {% endif %}

    {% if body_text %}
      <div class="card__body">
        {{ body_text }}
      </div>
    {% endif %}

    {% block tags %}
      {% if tags %}
        {%
          include '@training_theme/tags/tags.twig' with {
            "items": tags
          } only
        %}
      {% endif %}
    {% endblock tags %}

    {% block author %}
      {% if author %}
        {%
          include '@training_theme/author/author.twig' with {
            "author": author
          } only
        %}
      {% endif %}
    {% endblock author %}
  </div>
</article>
```
{% endtab %}
{% endtabs %}

## Integrating the Tags component

We will use the **Tags** Taxonomy vocabulary that comes out of the box with Drupal.

### Creating a view mode for the tags vocabulary

1. Go to the **Tags** _Manage Display_ screen and create a new view mode for Tags called **Blog**.  Creating a view mode for tags will allow us to create custom twig templates that will only affect tags in blog posts.  Typically tags look the same across an entire website, but there are times when some tags may need to look different depending where they appear.
2. After the view mode has been created be sure to enable it in the Tags vocabulary.
3. Hide the label for the description inside the **Blog** view mode.

### Update the Article content type

Now let's make a quick change to the Tags field in the Article content type so we can change the tag's format from Label to **Rendered entity**.

1. Go to the Article content type's **Teaser** view mode
2. Change the Tags fields format to `Rendered entity` and hide its label if not already done.
3. Change the Tags fields view mode to **Blog** by clicking the little cogwheel icon to the right of the Tags' field.
4. Be sure to click **Update** and then **Save**

### Template suggestions for Taxonomy terms

If you recall when we built the Tags component above we did it in two steps, first we built a single tag item, then we built a list of tags by including the single item in a loop. We will follow the same approach for integrating the component with Drupal. We will create a twig template suggestion for a single link item, then we will create another one to wrap the entire list of tags.

1. Inspect the tags found in the homepage From our blog section (right-click + Inspect)
2. Identify the twig template suggestions for taxonomy.  This will be the template for the individual tag item.

![Taxonomy term template suggestions.](../../.gitbook/assets/term.png)

The first template suggestions above give us 3 options. We are going to name our template `taxonomy-term--tags.html.twig`.

1. Go ahead and copy the source template from its original location into your theme's `/templates/content` folder.
2. Rename the copy of the template to match our desired name.

{% hint style="info" %}
Don't forget to clear Drupal's cache every time you add a new template to your theme.
{% endhint %}

The next template we need will be found just above the first one. The code looks like this:

![Tags field info.](../../.gitbook/assets/taxonomy-field.png)

As I mentioned before, we only want to affect tags that appear on blog posts. Looking at the list of options for template suggestions I can see that `field--node--field-tags--article.html.twig` (top one), is the one that gives us the more specific target. This template is for the Tags field in the Article content type and at the end it includes the view mode we just created for the Tags vocabulary, **blog**.

Go ahead and make a copy of this template from its original location into your theme's `/templates/field` folder, and rename it as we just discussed. This will be the template for the entire list of tags.

### Time to integrate the tags

1. Open `taxonomy-term--tags.html.twig` and remove all the code except the comments
2. Add the following code at the bottom of the template:

{% tabs %}
{% tab title="taxonomy-term--tags.html.twig" %}
```php
{% include '@training_theme/tags/tag-item.twig' %}
```
{% endtab %}
{% endtabs %}

* Since our tag item template (`tag-item.twig`) was built as a single link with variables for `url` and `name`, all we need to integrate it with Drupal is to include the template. No need for fields mapping because the taxonomy term template provides **url** and **name** by default.
* Open `field--node--field-blog-tags--blog.html.twig` and also remove all of the code except for the comments
* Add the following code at the bottom of the template:

{% tabs %}
{% tab title="field--node--field-blog-tags--blog.html.twig" %}
```php
{% embed '@training_theme/tags/tags.twig' %}
  {% block tag_item %}
    {{ item.content }}
  {% endblock %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

* Twig blocks to the rescue again.  We're embedding the tags component and using the `tag_item` twig block to pass the template's variables so they match what Drupal expects.

Now if you save your changes and clear Drupal's cache, reload the homepage and the regular cards will now displayed as shown in our designs.
