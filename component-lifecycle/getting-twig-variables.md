# Integrating the Hero

Now it's time to begin the integration process for the Hero component. We are going to break things down and explain each part separately.

### Exercise: Integrate the Hero

* Open `/src/templates/paragraphs/paragraph--hero.html.twig` in your text editor
* Remove all code in the file but leave all comments. It is good to leave the comments untouched as they provide helpful information regarding available variables and other useful Drupal-specific details.
* Add the following code at the bottom of the template:

{% tabs %}
{% tab title="paragraph--hero.html.twig" %}
```php
{% set rendered_content = content|render %}
```
{% endtab %}
{% endtabs %}

To follow best practices we discussed earlier regarding letting Drupal render the full content array, we are setting a twig variable for the sole purpose of triggering a full render of the content array. We are not going to use the variable at all, it is only intended to trigger Drupal to do its thing.

* Next step is to declare variables for the `title`, `eyebrow`, and `cta` fields. Although this is not required, it will make things look cleaner and more readable later on.  You'll see:

{% tabs %}
{% tab title="paragraph--hero.html.twig" %}
```php
{% set hero_title = {
    heading_level: '1',
    modifier: ' hero__title',
    title: content.field_title|render|trim is not empty ? content.field_title,
    url: ''
  }
%}

{% set hero_eyebrow = {
    text: content.field_eyebrow|render|trim is not empty ? content.field_eyebrow|field_value,
    modifier: ' hero__eyebrow'
  }
%}

{% set hero_cta = {
    text: content.field_cta|field_raw('title'),
    url: content.field_cta|field_raw('uri'),
    modifier: 'hero__cta'
  }
%}
```
{% endtab %}
{% endtabs %}

* Reason for setting variables for the fields above is that they all have several properties in addition to the actual value of the field. Setting these variables allow us to configure all their properties and their values prior to using the variables.
* The structure of these 3 variables matches the data structure in the components in Pattern Lab.  The biggest difference here is that for the **title** value \(line 4\), **text** value \(line 10\), **text** value \(line 16\), and **url** value \(line 17\), we are passing Drupal data.
* A good practice when getting field values is to strip white space by using the `|render|trim`Twig filters, and then check that the field is really not empty \(`is not empty ?`\) if that's true, we print the field's value \(i.e.`content.field_titile`\).

  Now let's make use of the Hero component in the Paragraph template. Let's look at the code below and explain how this works.

{% tabs %}
{% tab title="paragraph--hero.html.twig" %}
```php
{%
  include '@training_theme/hero/hero.twig' with {
    attributes: attributes,
    image: content.field_image|render|trim is not empty ? content.field_image,
    eyebrow: hero_eyebrow,
    heading: hero_title,
    body: content.field_body|render|trim is not empty ? content.field_body,
    cta: hero_cta
  } only
%}
```
{% endtab %}
{% endtabs %}

* We are using an `include` Twig statement to integrate the Hero component. Using  the  theme's namespace, `training_theme`, we are able to point  Drupal to our  theme's `src/patterns/components/hero/hero.twig`  template.  As  we mentioned before, by default Drupal only looks for Twig templates inside  `src/templates/`, but thanks to the  [Component Libraries](https://www.drupal.org/project/components) module and the namespace we created, we can  direct Drupal to also look for Twig templates in our components directory, among other places. **IMPORTANT**:  Change `training_theme` with your actual namespace.
* Next we pass in Drupal's `attributes` variable so that Drupal  can inject any attributes it needs to the Hero paragraph type.  This is recommended, but not required.
* The next step is to  map the `eyebrow, heading, and button` fields with  Drupal's equivalent of those fields.  While creating the variables above was not required nor needed, having done so makes  the mapping of keys to their values, much cleaner.
* Last but not least we map the `body` key with Drupal's body field and again, repeat the process to strip any white space in the field as well as ensuring the field is not empty.
* I lied, it's not last  😊 notice in the `include` statement after the twig template path there is a keyword `with`? and at the end of the block of code there is an `only` keyword?   These are Twig's helpful keywords that make it possible to limit the fields we want to display.  For example, if we  only wanted the hero to show a title and  body fields,  we could just include those fields and leave the others out.  For this to work the `with` and `only` keywords need to be present otherwise we would get errors when Drupal renders the Hero as it would expect all the other fields as well.

Once you've written all that code, the full component integration should look like this:

{% tabs %}
{% tab title="paragraph--hero.html.twig" %}
```php
{# Declares variable to trigger renderign of content array #}
{% set rendered_content = content|render %}

{# Setting variable for hero title #}
{% set hero_title = {
    heading_level: '1',
    modifier: ' hero__title',
    title: content.field_title|render|trim is not empty ? content.field_title,
    url: ''
  }
%}

{# Setting variable for hero eyebrow #}
{% set hero_eyebrow = {
    text: content.field_eyebrow|render|trim is not empty ? content.field_eyebrow|field_value,
    modifier: ' hero__eyebrow'
  }
%}

{# Setting variable for hero cta #}
{% set hero_cta = {
    text: content.field_cta|field_raw('title'),
    url: content.field_cta|field_raw('uri'),
    modifier: 'hero__cta'
  }
%}

{# Including hero component and mapping its fields to Drupal's fields #}
{%
  include '@training_theme/hero/hero.twig' with {
    attributes: attributes,
    image: content.field_image|render|trim is not empty ? content.field_image,
    eyebrow: hero_eyebrow,
    heading: hero_title,
    body: content.field_body|render|trim is not empty ? content.field_body,
    cta: hero_cta
  } only
%}
```
{% endtab %}
{% endtabs %}

## Change the field format for the button

By default Drupal is printing the button field as a single `<a>` tag. While this may work in some situations, it does not in this particular situation since we need the URL and button text values as two separate items.

* In your Drupal site, click **Structure \| Paragraph Types \| Hero**
* Click the **Manage Display** tab
* For the **Call To Action** field, change its format to **Separate field text and URL**.  Now the variable we set above will work.

## Displaying the integrated Hero in Drupal

If we clear Drupal's cache and reload the page we should see the Hero in Drupal inheriting all the styles and markup from the component in Pattern Lab.

_**You DID IT!**_ 🙌 🔥

Just for fun, once the hero displays in Drupal, inspect the code again and you should see all the markup we wrote when we built the component in Pattern Lab. This means Drupal is only providing the data for the component, but the markup, styles and javascript, if any, is sourced from Pattern Lab.

## But wait ...It didn't work 👎 😝

Perhaps the Hero component is rendering properly in Drupal, and the Markup when we inspect the code all looks like it's coming from Pattern Lab. But the Hero is broken as it has no styles at all. What went wrong? The answer is Drupal Libraries. Let's fix this problem now by talking about [Drupal Libraries](drupal-libraries.md).

