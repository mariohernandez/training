# Improving the Heading

The heading component looks good and it will work great, ...as long as we always want to use a `<h1>`. However, the component is pretty static and it does not offer much flexibility. What if we wanted to use a h2 or h3? or what if the title field is a link to another page? Then the heading component would probably not work because we have no way of changing the heading level from h1 to any other level or add a URL. Let's re-work the heading component so we make it more dynamic.

* Update `heading.json` to look like this:

{% tabs %}
{% tab title="heading.json" %}
```bash
{
  "heading": {
    "heading_level": "",
    "modifier": "",
    "title": "Welcome to the best training workshop!",
    "url": ""
  }
}
```
{% endtab %}
{% endtabs %}

We just created an object for the heading with key/value **heading\_level, modifier, title**, and **url**.

* The **heading\_level** is something we will use later as we start nesting the heading component into other components. This will allows us to change the headings from say, h1 to h2 if we need to.
* The **modifier** key allows us to pass a modifier CSS class when we make use of this component. The modifier class will make it possible for us to style the heading differently than other headings, if needed.
* the **title** key is the title's string of text that will become the title of a page or a component.
* ... and finally, the **url** key, if present, will allow us to wrap the title in an `<a>` tag, to make it a link.

## Update the heading's markup and logic

* Update the `heading.twig` file to look like this:

{% tabs %}
{% tab title="heading.twig" %}
```php
<h{{ heading.heading_level|default('2') }} class="heading{{ heading.modifier ? ' ' ~ heading.modifier }}">
  {% if heading.url %}
    <a href="{{ heading.url }}" class="heading__link">
      {{ heading.title }}
    </a>
  {% else %}
    {{ heading.title }}
  {% endif %}
</h{{ heading.heading_level|default('2') }}>
```
{% endtab %}
{% endtabs %}

Wow! What's all this? 😮

Let's break things down to explain what's happening here since the twig code has changed significantly:

* Line 1, makes use of `heading.heading_level` to complete the number part of the heading.  If a value is not provided for `heading_level` in the JSON file, we are setting a default of `2`.  This will ensue that by default we will have a `<h2>` as the title, much better than `<h1>` as we had before.  This value can be changed per use case if needed.  Line 9 closes the heading tag.
* Also in Line 1, we are checking whether there is a value for the `modifier` key in JSON.  If there is, we are passing it to the heading as a CSS class.  If no value is provided nothing will be added.
* In line 2, we check whether a URL was provided in the JSON file, and if so, we wrap the `{{ title }}` variable in a `<a>` tag to turn the title into a link.  The **href** value for the link is `{{ heading.url }}`.  If no URL is provided in the JSON file, we simply print the value of `{{ title }}`as plain text.

### Compiling the code

If Pattern Lab is running you should see the updates to the Heading component.  Otherwise run the commands below:

```text
npm run build
```

```text
npm run watch
```

**Just for fun 💥**

* Try changing the heading level in `heading.json` to anything other than H2.
* Inspect your code to see your changes to the Heading pattern.

**Congratulations!** You just built your first reusable component! 🙌 🎉

