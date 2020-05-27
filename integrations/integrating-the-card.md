# Integrating the Card

Our homepage is displaying blog posts that meet the requirements of the Drupal View we created, but they lack styles.  As we indicated before, each blog article will be represented by a Card component.  Let's integrate the Card so our articles inherit all the attributes of the component.Let's recap the work we've done and what the next steps are:

1. We built the Card component \(with the **Card Wide** variant\)
2. Created a Blog content type with designated View Modes \(**Full content, Featured, & Teaser**\)
3. We created a Drupal View to generate the blog listing sections in our homepage
4. Finally, we created several blog posts to populate the homepage

#### Next steps:

We'll get back to the full view of a blog post later, for now we are going to focus on associating the Card component with the Teaser view mode, and the Card Wide variant with the Featured view mode.  How do we do this?  The answer is Twig template suggestions.

### Exercise: Creating twig templates for blog posts

1. In your Drupal site, navigate to the Homepage node
2. Right-click on any of the Blog posts articles within the _From our blog_ section, and select **Inspect** or **Inspect Element**
3. Scroll up in the inspector's code until you find the `<article>` element that wraps the entire article you clicked on.  There may be multiple `<article>` tags within each article, but ensure you are looking at the main article wrapper.  See screenshot below \(click on it to zoom in\):

![Example of debugging info for a node](../.gitbook/assets/node-teaser.png)

* I've marked a couple of important items in the screenshot above to ensure you are looking at the correct section in the code.
* **THEME HOOK:** Tells you what entity you are currently looking at.  In this example we are looking at the **node**, which is what we want since we are trying to configure the Blog nodes with the right component.
* Next I have outlined all the possible template FILE NAME SUGGESTIONS Drupal is telling us we can use for this particular type of node.  We know we are looking at a node as all the template suggestion names start with the word **node--\***.  We can get as specific or general as we need to.
* Finally, I have pointed out where the current template being used \(`node.html.twig`\) is located.

{% hint style="info" %}
**IMPORTANT:** To ensure we are all following along with the same article type, please ensure you selected an article from the _From our blog_ collection of articles.  This means you should see the word `teaser` somewhere in the list of template names above.  If don't see it, close your code inspector and repeat steps 2 & 3 above with a different article.
{% endhint %}

#### Creating a template suggestion for Blog teaser view mode

The focus at this point is to create template suggestions for all article nodes that will be displayed in the **Teaser** view mode.  So if we look at the list of file name suggestions above we can ignore the top 4 names as those are either related to the full section of content or are extremely specific to only the single article we are looking at \(**node--6\***\).

1. So based on the remaining names after ignoring the first 4, we can select the following name: `node--blog--teaser.html.twig`.  This names is exactly what we need to style all blog nodes that will be displayed in teaser view mode.
2. Now that we've selected the template we need, let's create it by making a copy from `core/themes/stable/templates/content/node.html.twig` into your theme's templates directory \(`/themes/custom/training_theme/src/templates/content/`
3. Rename the newly copied template as `node--blog--teaser.html.twig`
4. Click your Drupal's cache

{% hint style="info" %}
I know I will be creating other node related template suggestion so I will leave the copy of `node.html.twig` unchanged in my /templates folder so I can keep making copies of it.
{% endhint %}

If you reload the homepage, you shouldn't really notice much difference.  However, if you right-click on the same article as you did before and select **Inspect** or **Inspect Element**, and scroll to the `<article>` element, you should see your new template being used by Drupal to render some of the blog nodes.  See below for an example:

![Example of using teaser view mode for blog nodes.](../.gitbook/assets/node-blog-teaser.png)

### Integrating the Card component

OK, now that our custom twig template is ready, it's time to plug it to our Card component so our blog posts start looking nice.

We'll break the integration process down so we can explain each part of it.  You will find the full template at the bottom of this page.

1. Open **node--blog--teaser.html.twig** in your editor and remove all its code except for the comments at the top of the template
2. At the bottom of the template, add the following code:
  {% tabs %}
  {% tab title="node--blog--teaser.html.twig" %}
  ```php
  {% set rendered_content = content|render %}
  ```
  {% endtab %}
  {% endtabs %}
  * First thing we are setting a twig variable to trigger a full render of the content variable
3. Now let's create twig variable for the card's title field
  {% tabs %}
  {% tab title="node--blog--teaser.html.twig" %}
  ```php
  {% set article_title = {
      "heading_level": 3,
      "modifier": "card__title",
      "title": label,
      "url": url
    }
  %}
  ```
  {% endtab %}
  {% endtabs %}
  * Why are we doing this?  Well, Drupal only gives us the value of the title text and its url.  We are setting a variable so we can construct the title the same way we did when we built the heading component (heading_level and modifier).
4. Now, let's embed the Card component as follows:
  {% tabs %}
  {% tab title="node--blog--teaser.html.twig" %}
  ```php
  {% embed '@training_theme/card/card.twig' with
    {
      "attributes": attributes,
      "title_prefix": title_prefix,
      "title_suffix": title_suffix,
      "image": content.field_blog_image|render|trim is not empty ? content.field_blog_image,
      "title": article_title,
      "date": date,
      "body_text": content.body|render|trim is not empty ? content.body,
      "tags": content.field_blog_tags,
      "modifier": ""
    }
  %}

    {% block card_date %}
      {{ date }}
    {% endblock card_date %}

    {% block tags %}
      {{ tags }}
    {% endblock tags %}
  {% endembed %}
  ```
  {% endtab %}
  {% endtabs %}
  * Why use `embed` and not `include`?  Twig gives us 3 ways to nest or "include" templates/components into other twig templates; `include`, `extends`, and `embed`.  Each have their pros/cons.  You can [learn more about them](https://github.com/fourkitchens/emulsify/wiki/When-to-use-include,-extends,-and-embed).
  We need to use `embed` instead of `include` to be able to use the twig blocks for date and tags at the bottom of the code snippet above.
  * The first 3 items inside the `embed` statement above are Drupal specific variables so we laverage Drupal's use of `attributes`, `title_prefix` and `title suffix`.  Adding these items will allows us to do quick edit of content among other things.
  * Next we are mapping the Image variable from the Card component to Drupal's image field by first ensuring the field is really not empty.
  * Then we are making use of the `article_variable` we created.  Although creating this variable was not needed, it sure make things look cleaner inside the embed block.
  * The we map the date and tags elements.  For the tags we are mapping the variable `tags` with Drupal's taxonomy entity (`content.field_blog_tags`).  This is only half the job.  More on this shortly.
  * **Twig blocks**: So mapping each of the components with Drupal's respective fields is only half the job.  At least for the date and tags fields in this case.  Using Twig blocks at the bottom of the embed, we can now pass the values for the elements we want to render when using this template.  In the case of the date, we are using the twig block called `card_date`.  If you remember, we also created another twig block for date but that will be used in the Card Wide variant.  Using twig blocks here allows us to pick which and where we want the content.  Let's say we used the `featured_date` twig block instead, then the date info will be displayed in the top left corner of each card as it currently does in the Card Wide variant.

  As for the `tags` twig block, we also first mapped the variable from the component to Drupal's tags entity, then in the twig block we are telling it to print them.
