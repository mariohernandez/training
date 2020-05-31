# Integrating Featured Content

## Integrating Featured Content

Now let's repeat what we just did with the From our blog section, with the Featured Content.

In this case we will only create one view template suggestion, only for the Featured content block `views-view--blog-posts--featured-content.html.twig`. Since both blocks \(**from-our-blog** & **featured-content**\), are part of the same view \(Blog posts\), and they both use the same data format of `unformatted` , we can use the same template for both blocks. This means `views-view--unformatted--blog-posts.html.twig` will serve both sections of content.

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

If we look at the homepage we can see all the content is displaying as expected with the exception of the images in the two types of cards. We are going to fix this so all images for each type of card display consistent width and height. We are going to use the power of images styles, responsive image styles, and view modes. Let's do this now.

## Integrating Featured Content

In the past two integration exercises we have integrated components with data that is coming from a content type. This time we are going to integrate the movie card collection component with data that is coming from a Drupal view. The process is a little different as Drupal's view offer their own twig templates and the data they produce is usually a collection of fields or list of fields.

### Views template suggestions

Whether data for a component comes from a content type, paragraph, block or a view, we still need to be able to override Drupal's templates in order to integrate the components, which means we need to create custom twig template suggestions.

Views template suggestions are not as straight forward as the ones we have worked with thus far. Here is some info on [views template suggestion](https://api.drupal.org/api/drupal/core!modules!views!views.theme.inc/group/views_templates/8.2.x) you should get acquainted with. In addition, [this article](http://redcrackle.com/blog/drupal-8/theme-views-templates) provides a great breakdown on how Views template suggestions work.

One key piece of information in the views article above is this:

> For each view, there will be a minimum of **two templates** used. The first is used for all views: `views-view.html.twig`. The second template is determined by the style selected for the view \(i.e. unformatted, fields, etc.\), for which a template suggestion would look like `views-view-unformatted.html.twig`. Note that certain aspects of the view can also change which style is used; for example, arguments which provide a summary view might change the style to one of the special summary styles.

### Discovering the right views template to override

The process for discovering the templates Drupal's views are using is the same as what we've done so far, twig debugging. So repeat the same process as follows:

1. Go to the site's homepage \(/homepage\), where the movie list is displayed
2. Right-click on any of the movies within the list and select **Inspect** or **Inspect Element** depending on your browser.
3. Within the code inspector, scroll up until you find template suggestions starting with **views-view--**. Example:

![Example of twig debug showing views templates](../.gitbook/assets/views-1.png)

As we read in the excerpt above, there are usually two views templates using when rendering content, the first one I'd like to think of as the wrapper for the view and the second one wraps the content or content rows, and its name is based on the display format used when creating the view \(i.e. unformatted\). This is what we are seeing in the screenshot above.

### Creating Views template suggestions

1. Copy the `views-view.html.twig` and `views-view-unformatted.html.twig` files from `/core/themes/stable/templates/views/`, and place them into `<project-root>/web/themes/custom/<theme-name>/src/templates/views/` If the **views** directory does not exist, create it.
2. We need to rename the templates as follows:
   * `views-view--featured-content.html.twig` and `views-view-unformatted--featured-content.html.twig`
   * If you are wondering where **featured-content** comes from, that's the name of the view we created \(machine name `latest_posts`\).
   * You can find a View's machine name on the main views admin page \(/admin/structure/views\)
3. Clear Drupal's cache
4. If you reload the /news page, you will not see any visual changes on the content but if you inspect the page again you will notice that Drupal is now using the newly created template suggestions.
5. In your editor open `views-view--featured-content.html.twig` and add the following code overriding the existing code in the template \(except for the comments as we would like to keep the comments intact\):

{% tabs %}
{% tab title="views-view--featured-content.html.twig" %}
```php
{%
  set classes = [
    dom_id ? 'js-view-dom-id-' ~ dom_id,
  ]
%}

{% set attributes = attributes.addClass(classes) %}

{% embed '@training_theme/featured-content/featured-content.twig' %}
  {% block latest_posts %}
    {{ rows }}
  {% endblock %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

* First, we're keeping the `dom-id` class that views adds, and updating the `attributes`variable for the view to include that class. This will help keep classes intact that views and/or other modules may rely on.
* Next, we're using the twig embed statement again to map the content of this view to our **Featured Content** component, and passing in Drupal attributes so that they'll be output with our component's markup.
* For the twig block we named `latest_posts` in the **Featured Content** component, we output the `rows` variable that views provides, which is basically the content of this view, plus the `title_prefix` and `title_suffix` variables.
* In your editor open **views-view-unformatted--lastest-posts.html.twig** and add the following code overriding the existing code in the template \(except for the comments as we would like to keep the comments intact\):

{% tabs %}
{% tab title="views-view-unformatted--featured-content.html.twig" %}
```php
{% for row in rows %}
  {{- row.content -}}
{% endfor %}
```
{% endtab %}
{% endtabs %}

* There is very little going on here. We've stripped most of the code from the original template, but why? Well, if you look at the **featured content** component, you will see that we already have everything we need as far as Drupal requirements for rendering content and Drupal specific attributes. So in this template we are simply cleaning up the code to avoid printing any extra stuff we don't need.
* As you may recall, in the **featured content** component, the data for individual **cards** is stored in an `items[ ]` array in the component's `.json` file. We loop through that array, and for each item we use an `include` statement to add a **card** component and pass in the data from the item we're currently iterating over. This gives us a list of movie cards inside our markup for the **Featured Content** component.
* Views is essentially doing the same thing. The `latest_posts` view is set up to show a list of article nodes displayed in the teaser view mode. Since we already integrated the **card** with the teaser view mode of article nodes, the end result is the same: a simple list of movie cards.

#### Clear Drupal's caches

Now if you reload the /news page you should see the featured content in place. There is one more thing to do for the listing of movies and we will do that next.

