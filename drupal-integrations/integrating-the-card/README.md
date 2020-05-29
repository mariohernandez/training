# Integrating the Card

![Default card component](../../.gitbook/assets/card.png)

Our homepage is displaying blog posts that meet the requirements of the Drupal View we created, but they lack styles. As we indicated before, each blog article will be represented by a Card component. Let's integrate the Card so our articles inherit all the attributes of the component.Let's recap the work we've done and what the next steps are:

1. We built the Card component \(with the **Card Wide** variant\)
2. Created a Blog content type with designated View Modes \(**Full content, Featured, & Teaser**\)
3. We created a Drupal View to generate the blog listing sections in our homepage
4. Finally, we created several blog posts to populate the homepage

#### Next steps:

We'll get back to the full view of a blog post later, for now we are going to focus on associating the Card component with the Teaser view mode, and the Card Wide variant with the Featured view mode. How do we do this? The answer is Twig template suggestions.

### Exercise: Creating twig templates for blog posts

1. In your Drupal site, navigate to the Homepage node
2. Right-click on any of the Blog posts articles within the _From our blog_ section, and select **Inspect** or **Inspect Element**
3. Scroll up in the inspector's code until you find the `<article>` element that wraps the entire article you clicked on.  There may be multiple `<article>` tags within each article, but ensure you are looking at the main article wrapper.  See screenshot below \(click on it to zoom in\):

![Example of debugging info for a node](../../.gitbook/assets/node-teaser.png)

* I've marked a couple of important items in the screenshot above to ensure you are looking at the correct section in the code.
* **THEME HOOK:** Tells you what entity you are currently looking at.  In this example we are looking at the **node**, which is what we want since we are trying to configure the Blog nodes with the right component.
* Next I have outlined all the possible template FILE NAME SUGGESTIONS Drupal is telling us we can use for this particular type of node.  We know we are looking at a node as all the template suggestion names start with the word **node--\***.  We can get as specific or general as we need to.
* Finally, I have pointed out where the current template being used \(`node.html.twig`\) is located.

{% hint style="info" %}
**IMPORTANT:** To ensure we are all following along with the same article type, please ensure you selected an article from the _From our blog_ collection of articles. This means you should see the word `teaser` somewhere in the list of template names above. If don't see it, close your code inspector and repeat steps 2 & 3 above with a different article.
{% endhint %}

#### Creating a template suggestion for Blog teaser view mode

The focus at this point is to create template suggestions for all article nodes that will be displayed in the **Teaser** view mode. So if we look at the list of file name suggestions above we can ignore the top 4 names as those are either related to the full section of content or are extremely specific to only the single article we are looking at \(**node--6\***\).

1. So based on the remaining names after ignoring the first 4, we can select the following name: `node--blog--teaser.html.twig`.  
   1. **node** is the Drupal entity we are trying to integrate with
   2. **blog** is the content type \(also an entity\)This names is exactly what we need to style all blog nodes that will be displayed in teaser view mode.
2. Now that we've selected the template we need, let's create it by making a copy from `core/themes/stable/templates/content/node.html.twig` into your theme's templates directory \(`/themes/custom/training_theme/src/templates/content/`
3. Rename the newly copied template as `node--blog--teaser.html.twig`
4. Click your Drupal's cache

{% hint style="info" %}
I know I will be creating other node related template suggestion so I will leave the copy of `node.html.twig` unchanged in my /templates folder so I can keep making copies of it.
{% endhint %}

If you reload the homepage, you shouldn't really notice much difference. However, if you right-click on the same article as you did before and select **Inspect** or **Inspect Element**, and scroll to the `<article>` element, you should see your new template being used by Drupal to render some of the blog nodes. See below for an example:

![Example of using teaser view mode for blog nodes.](../../.gitbook/assets/node-blog-teaser.png)

### Integrating the Card component

OK, now that our custom twig template is ready, it's time to plug it to our Card component so our blog posts start looking nice.

We'll break the integration process down so we can explain each part of it. You will find the full template at the bottom of this page.

1. Open **node--blog--teaser.html.twig** in your editor and remove all the code except for the comments at the top of the template
2. At the bottom of the template, add the following code:

   ```php
   {% set rendered_content = content|render %}
   ```

   First thing we are setting a twig variable to trigger a full render of the content variable

3. Now let's create twig variable for the card's title field

   ```php
   {% set article_title = {
      "heading_level": 3,
      "modifier": "card__title",
      "title": label,
      "url": url
    }
   %}
   ```

   Why are we doing this? Well, Drupal gives us the article title text and url, but we still need to add a modifier class and a heading level. We are setting a variable so we can construct the title the same way we did when we built the heading component.

4. Now, let's add an `embed` statement for the Card component:

   ```php
   {% embed '@training_theme/card/card.twig' with { ... } %} {% endembed %}
   ```

   Why use `embed` and not `include`? Twig gives us 3 ways to nest or "include" templates/components into other twig templates; `include`, `extends`, and `embed`. Each have their pros/cons. You can [learn more about them](https://github.com/fourkitchens/emulsify/wiki/When-to-use-include,-extends,-and-embed). We need to use `embed` instead of `include` to be able to use the twig blocks we added in the Card component for the `date` and `tags` fields

5. Now let's start mapping the card's variables with Drupal fields or variables.

   ```php
   {% embed '@training_theme/card/card.twig' with
    {
      "attributes": attributes,
      "title_prefix": title_prefix,
      "title_suffix": title_suffix,
      ...
    }
   %}

   {% endembed %}
   ```

   The first 3 items inside the `embed` statement above are Drupal specific variables so we laverage Drupal's use of `attributes`, `title_prefix` and `title suffix`. Adding these items will allows us to make use of Drupal's contextual links to quickly edit content as well as allowing Drupal to add its attributes to our component's markup.

6. Let's now make use of the `article_title` variable we created above

   ```php
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

   {% endembed %}
   ```

   Next we are mapping the `image`, `date`, `body_text`, and `tags` variables with Drupal fields for those elements but first we check that the fields are not empty.

7. Time to add the twig blocks for the date and the tags

   ```php
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

    {% block card_date %}
      {{ date }}
    {% endblock card_date %}

    {% block tags %}
      {{ tags }}
    {% endblock tags %}
   {% endembed %}
   ```

   Mapping each of the components with Drupal's equivalent fields is only half the job. At least for the date and tags fields in this case. By using Twig blocks we can explicitly declare the data we want to render in the cards. If you remember, we created two twig blocks for the date field. One for the regular card and one for the card wide. Twig blocks in the embed statement above let us pick which of the two we want to use. The one not used above will be completely ignored when Drupal renders the card.

### Rendering blog nodes as cards in Drupal

Now that the card integration is complete, let's take a look at how the blog nodes look in Drupal.

1. After saving all your changes to **node--blog--teaser.html.twig**, clear Drupal's cache
2. Reload the homepage

### Custom date formats

The card looks great but it looks like the date format does not match our designs. Also the tags are not styled at all.  Let's fix these two issues.

1. In Drupal, click on **Configuration &gt; Regional and language &gt; Date and time formats**
2. Click **Edit** next to **Default long date**
3. In the **Format string** field, update its value with `l, F j, Y`
4. Click **Save format**
5. Repeat these steps with **Default short date** and replace its value with `F j`
6. Save your changes.

## Update the date format in the teaser template

Now that we've updated Drupal's date formats, let's make use of one of them. We will use the other one when we integrate the card wide variant.

1. Add the following code in `node--blog--teaser.html.twig`

{% tabs %}
{% tab title="node--blog--teaser.html.twig" %}
```php
{% set date = node.createdtime|format_date('long') %}
```
{% endtab %}
{% endtabs %}

* We are setting a variable for date to change its format to the **long** format we just setup.

### Exercise: Integrate the Taxonomy terms \(tags\)

Taxonomy are Drupal entities just like Nodes, blocks, etc.  This means we can create view modes and custom templates so we can integrate them with Drupal.  Currently we don't have a component for displaying tags.  Let's quickly build one.

#### Build a component for the tags

1. Inside `src/patterns/components/` create a new folder called **tags**
2. Inside the _tags_ folder create a new file called `_tag-item.twig` \(_notice the underscore in the file name_\).  Using an underscore in-front of a twig file name allows [Pattern Lab to ignore the file](https://patternlab.io/docs/hiding-patterns-in-the-navigation/).  We don't need to see an individual tag in Pattern Lab, we need to see the full collection of tags.  More on this shortly.
3. Add the following code inside `_tag-item.twig`

{% tabs %}
{% tab title="\_tag-item.twig" %}
```php
{% block tag_link %}
  <a href="{{ url }}" class="tag__link">
    {{ name }}
  </a>
{% endblock %}
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

<ul class="tags"{{ attributes }}>
  {{ title_prefix }}
  {{ title_suffix }}
  {% block blog_categories %}
    {% for item in items %}
      <li class="tag__item">
        {%
          include '@training_theme/tags/_tag-item.twig' with {
            "name": item.name,
            "url": item.url
          } only
        %}
      </li>
    {% endfor %}
  {% endblock %}
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
  background-color: $color-catskill-white;
  border-radius: 99999px;
  color: $color-gray-dark;
  display: inline-block;
  margin-right: 10px;

  a {
    color: lighten($color-gray-dark, 25%);
    display: inline-block;
    font-size: 1.3rem;
    line-height: 1.2;
    padding: 2px 10px;
    text-decoration: none;

    &:hover,
    &:focus {
      color: $color-gray-dark;
    }
  }
}
```
{% endtab %}
{% endtabs %}

* If you save your changes and compile your code you should see a list of tags in Pattern Lab.  Let's integrate this component with Drupal now to fix our tags inside the card of blog posts.

### Integrating the Tags component with Taxonomies

We will use the **Tags** Taxonomy vocabulary that comes out of the box with Drupal.

#### Creating a view mode for the tags vocabulary

1. Go to the **Tags** _Manage Display_ screen and create a new view mode for Tags called **Blog**.  Creating a view mode for tags will allow us to create a custom twig template that will only affect tags in blog posts.  Typically tags look the same across an entire website, but there are times when some tags may need to look different depending where they appear.
2. After the view mode has been created be sure to enable it in the Tags vocabulary.
3. Hide the label for the description inside the **Blog** view mode.

#### Update the Blog content type

Now let's make a quick change to the Tags field in the Blog content type so we can change the tag's format from Label to **Rendered entity**.

1. Go to the Blog content type's **Teaser** view mode
2. Change the Tags fields format to `Rendered entity` and hide its label if not already done.
3. Change the Tags fields view mode to **Blog** by clicking the little gear icon to the right of the Tags' field.
4. Be sure to click **Update** and then **Save**

#### Template suggestions for Taxonomy terms

If you recall when we built the Tags component above we did it in two steps, first we built a single tag item, then we built a list of tags by including the single item in a loop.  We will follow the same approach for integrating the component with Drupal.  We will create a twig template suggestion for a single link item, then we will create another one to wrap the entire list of tags.

1. Inspect the tags found in the homepage From our blog section \(right-click + Inspect\) 
2. Identify the twig template suggestions for taxonomy.

![Taxonomy term template suggestions.](../../.gitbook/assets/term.png)

The first template suggestions above give us 3 options.  We are going to name our template `taxonomy-term--tags.html.twig`.  

1. Go ahead and copy the source template from its original location into your theme's `/templates/content` folder.  
2. Rename the copy of the template to match our desired name.  

{% hint style="info" %}
Don't forget to clear Drupal's cache every time you add a new template to your theme.
{% endhint %}

The next template we need will be found just above the first one. The code looks like this:

![Tags field info.](../../.gitbook/assets/taxonomy-field.png)

As I mentioned before, we only want to affect tags that appear on blog posts.  Looking at the list of options for template suggestions I can see that `field--node--field-blog-tags--blog.html.twig` \(top one\), is the one that gives us the more specific target.  This template is for the Tags field in the blog content type and at the end it includes the view mode we just created for the Tags vocabulary, **blog**.

Go ahead and make a copy of this template from its original location into your theme's `/templates/field` folder, and rename it as we just discussed.

#### Time to integrate the tags

1. Open `taxonomy-term--tags.html.twig` and remove all the code except the comments
2. Add the following code at the bottom of the template:

{% tabs %}
{% tab title="taxonomy-term--tags.html.twig" %}
```php
{% if name and not page %}
  {% include '@training_theme/tags/_tag-item.twig' with {
      "name": name,
      "url": url
    } only
  %}
{% endif %}
```
{% endtab %}
{% endtabs %}

* We're leaving the `if` statement the template provided and are replacing its code with a twig `include` statement to nest the individual tag item we created in Pattern Lab.
* Then we are mapping the `name` and `url` properties with Drupal's equivalents.  If you look at the template's comments you will see this template already provides these two properties for us.

1. Open `field--node--field-blog-tags--blog.html.twig` and also remove all of the code except for the comments
2. Add the following code at the bottom of the template:

{% tabs %}
{% tab title="field--node--field-blog-tags--blog.html.twig" %}
```php
<ul{{ attributes.addClass('tags')}}>
  {% for item in items %}
    <li{{ item.attributes.addClass('tag__item') }}>
      {% embed '@training_theme/tags/_tag-item.twig' %}
        {% block tag_link %}
          {{ item.content }}
        {% endblock %}
      {% endembed %}
    </li>
  {% endfor %}
</ul>
```
{% endtab %}
{% endtabs %}

* You should be ashamed of yourself for doing what you just did above 🤣
* If you've been paying attention in training you would remember that I mentioned before that a presenter template \(like the one above\), should not have any HTML/markup.  It should only provide the data for our component.  So why did we do this?  Well, it's not terribly bad.  We're still using all of Drupal's attributes, but I was having a hard time getting the integration to work cleanly.
* Ideally we should just be able to include or embed the `tags.twig` template and that's it.  But I couldn't figure it out.  I'm sure I can figure it out but I was already spending too much time on this and I figured this was not so bad 🙈.
* Your mission, should you choose to accept it, is to fix this at some point.  Not now though.
* After reloading the homepage the tags should now look like in our designs.  Great job! 🙌

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

  {# Calls card_date twig block.#}
  {% block card_date %}
    {{ date }}
  {% endblock card_date %}

  {# Calls tags twig block.#}
  {% block tags %}
    {{ tags }}
  {% endblock tags %}
{% endembed %}
```
{% endtab %}
{% endtabs %}

You deserve a 🏆 This was quite the exercise.  Now, let's repeat all the steps on this page to integrate the Card Wide.  Let's go!

