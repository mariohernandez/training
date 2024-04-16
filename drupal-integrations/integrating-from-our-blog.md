# Integrating From our blog

Now let's work on integrating an entire section of components.  We just integrated the individual cards so each blog post is displayed using the card variant we selected.  Let's now integrate the **From our blog** section so we get the cards aligned in a row.

This integration will be different than what we've done thus far.  We'll be dealing with Drupal's views, which can be more difficult to figure out when it comes to creating Twig template suggestions.

## Views template suggestions

Whether data for a component comes from a content type, paragraph, block or a view, we still need to be able to override Drupal's templates in order to integrate the components, which means we need to create custom twig template suggestions.

Views template suggestions are not as straight forward as the ones we have worked with thus far. Here is some info on [views template suggestion](https://api.drupal.org/api/drupal/core!modules!views!views.theme.inc/group/views_templates/8.2.x) you should get acquainted with.  In addition, [this article](http://redcrackle.com/blog/drupal-8/theme-views-templates) provides a great breakdown on how Views template suggestions work.

One key piece of information in the views article above is this:

> For each view, there will be a minimum of **two templates** used. The first is used for all views: `views-view.html.twig`. The second template is determined by the style selected for the view (i.e. unformatted, fields, etc.), for which a template suggestion would look like `views-view-unformatted.html.twig`. Note that certain aspects of the view can also change which style is used; for example, arguments which provide a summary view might change the style to one of the special summary styles.

## Discovering the right views template to override

The process for discovering the templates Drupal's views are using is the same as what we've done so far, twig debugging. So repeat the same process as follows:

1. Go to the site's homepage where the blog posts are displayed
2. Right-click on any of the posts within the **From our blog **list and select **Inspect** or **Inspect Element** depending on your browser.
3. Within the code inspector, scroll up until you find template suggestions starting with **views-view--**. Example:

![Views twig templates](../.gitbook/assets/views.png)

As we read in the excerpt above, there are usually two views templates using when rendering content, the first one I'd like to think of as the wrapper for the view and the second one wraps the content or content rows, and its name is based on the display format used when creating the view (i.e. unformatted). This is what we are seeing in the screenshot above.

## Creating Views template suggestions

Using the same method as before to create new template suggestions, follow these steps:

1. Copy the `views-view.html.twig` and `views-view-unformatted.html.twig` files from `/core/themes/stable/templates/views/`, and place them into `/themes/custom/storybook/src/templates/views/`
2. Rather than renaming these templates, let's first make copies of them because we will need them again when we work in the **Featured Content** list later on.  Name each of the copies as follows:
   * `views-view--blog-posts--from-our-blog.html.twig` and `views-view-unformatted--blog-posts.html.twig`
   * If you are wondering where these names come from, let's explain:  **blog-posts** is the name we used when we created the Blog Posts view.  **from-our-blog** is the views block machine name.  This is why is important to assign custom machine names that make sense so when is time to create template suggestion, their names also makes sense.  Had we not changed each of our view's blocks machine names we would had ended up with **views-view--blog-posts--block-1.html.twig** as our template name.
   * You can find a View's machine name on the main views admin page (/admin/structure/views)
3. Clear Drupal's cache.
4. If you reload the homepage, you will not see any visual changes on the content but if you inspect the page again you will notice that Drupal is now using the newly created template suggestions.

### Reviewing the original templates

Before we override the templates let's take a look at some of the elements of the templates as these are extremely critical to a successful integration.  Let's start with `views-view--blog-posts--from-our-blog.html.twig`:

* This template is the wrapper of the entire view and the items being queried by the view. Think of this template as all the articles in the `items []` array when we created the **From our blog** component.
* `{{ title }}` this is the view's title which we have customized to show the section title such as **From our blog** or **Featured content**.  Although we could print this title, we are going to opt to instead print the the View's title through the block itself which will allow content editors to change the title of each section if needed.
* `{{ rows }}` are the actual nodes that are returned from the view's query.  Basically rows represent a list of article nodes.  This is probably the only thing we need from this template as we don't need `header`, `exposed`, `pager` or any of the other available variables in the template.

Now let's take a look at `views-view--unformatted--from-our-blog.html.twig`:

* This template is the one that produces the result of a single item in the view.  Think of this template as each individual item inside the `items []` array in the **From our blog** component.  Basically each item is a node as a card.
* `{% for row in rows %}` is the function that iterates through the `rows []` array and returns a single item or node.
* `{{ item.content }}` renders a single node article on the page

It is extremely important to understand the role of each template that interact with our components because this determines not only how our components are built but how our components relate to each of the templates.  In a moment we will see why when we built the **From our blog** component we split it into two parts; one for the node list and the other part for the block that will wrap the list and the list title.

### Integrating the view's main wrapper template

1. In your editor open `views-view--blog-posts--from-our-blog.html.twig `and add the following code overriding the existing code in the template (except for the comments as we would like to keep the comments intact):

{% tabs %}
{% tab title="views-view--blog-posts--from-our-blog.html.twig" %}
```php
{%
  set classes = [
    dom_id ? 'js-view-dom-id-' ~ dom_id,
  ]
%}

{% set attributes = attributes.addClass(classes) %}

{# Variable for cta #}
{% set cta = {
    modifier: '',
    text: 'Read more articles',
    url: '/blog'
  }
%}

{# Variable for the view title #}
{% set heading = {
    "heading_level": '2',
    "modifier": 'heading--large center section-header',
    "title": 'From our blog',
    "url": ''
  }
%}

{% embed '@storybook/from-our-blog/from-our-blog.twig' %}
  {% block blog_items %}
    {{ rows }}
  {% endblock %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

* First, we're keeping the `dom-id` class that views adds, and updating the `attributes`variable for the view to include that class. This will help keep classes intact that views and/or other modules may rely on.
* Next we are setting a variable for the **CTA** button so we can manually add the value to each of its properties.
* We are then doing the same for the section's title, by passing some helper CSS classes as well as the fixed title, **From our blog**.  As long as the variables we are setting match the ones found in the component we are integrating, the integration process looks cleaner.  If variable names for **cta** and **heading** did not match those in **from-our-blog.twig**, we would need to do a little more work inside the twig embed to map things by hand.
* Then we use a twig embed statement to include the **from-our-blog.twig** component.
* Finally, Drupal provides the `rows` variable which basically provides the result of the view's query. In this case the result is a list of blog post articles. Since we've already integrated the Card component with the node Article for individual blog articles, Drupal's views will provide us a list of Article posts each of which will automatically display already styled as a card.  We are passing Drupal attributes so that they'll be output with our component's markup.

### Integrating the view's individual item template (unformatted)

1. In your editor open **views-view-unformatted--blog-posts.html.twig** and add the following code overriding the existing code in the template (except for the comments as we would like to keep the comments intact):

```php
{% for row in rows %}
  {{- row.content -}}
{% endfor %}
```

* There is very little going on here. We've stripped most of the code from the original template, but why? Well, if you look at the **From our blog** component, you will see that we already have everything we need as far as Drupal requirements for rendering content and Drupal specific attributes. So in this template we are simply cleaning up the code to avoid printing any extra markup we don't need.
* As you may recall, in the **From our blog** component, the data for individual blog posts is stored in an `items[ ]` array in the component's `.json` file. We loop through that array, and for each item we do an `include` of a **card** and pass in the data from the item we're currently iterating over. This gives us a list of movie cards inside our markup for the **From our blog** component.
* Views is essentially doing the same thing. The `blog-posts` view is set up to show a list of blog nodes displayed in the teaser view mode. Since we already integrated the **card** with the teaser view mode, the end result is the same: a simple list of movie cards.

### Rendering the From our blog section

* Save your changes and clear Drupal's cache
* Now if you reload the homepage you should see the From our blog section nicely styled.

Next we will repeat the steps above with the **Featured content** section.
