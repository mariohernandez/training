# Improving the Title

The title component looks good and it will work great, ...as long as we always want to use a `<h1>`. However, the component is pretty static and it does not offer much flexibility. What if we wanted to use a h2 or h3? or what if the title field is a link to another page? Then the title component would probably not work because we have no way of changing the title level from h1 to any other level or add a URL. Let's re-work the title component so we make it more dynamic.

* Update `yml` to look like this:

{% tabs %}
{% tab title="yml" %}

```yml
---
level: ''
modifier: ''
text: 'Welcome to Mediacurrent training!'
url: ''
```

{% endtab %}
{% endtabs %}

We just created a JSON object for the title with properties that include **level, modifier, text**, and **url**.

* The **level** is something we will use later as we start nesting the title component into other components. This will allow us to change the titles from say, h1 to h2 if we need to.
* The **modifier** key allows us to pass a modifier CSS class when we make use of this component. The modifier class will make it possible for us to style the title differently than other titles, if needed.
* the **text** key is the title's string of text that will become the title of a page or a component.
* ... and finally, the **url** key, if present, will allow us to wrap the title in an `<a>` tag, to turn it into a link.

## Update the title's markup and logic

* Update the `title.twig` file to look like this:

{% tabs %}
{% tab title="title.twig" %}

```php
<h{{ level|default('2') }} class="title{{ modifier ? ' ' ~ modifier }}">
  {% if url %}
    <a href="{{ url }}" class="title__link">
      {{ title }}
    </a>
  {% else %}
    {{ title }}
  {% endif %}
</h{{ level|default('2') }}>
```

{% endtab %}
{% endtabs %}

Wow! What's all this? 😮

Let's break things down to explain what's happening here since the twig code has changed significantly:

* Line 1, makes use of `level` to complete the number part of the   If a value is not provided for `level` in the JSON file, we are setting a default of `2`.  This will ensure that by default we will have a `<h2>` as the title, much better than `<h1>` as we had before.  This value can be changed per use case if needed.  Line 9 closes the title tag.
* Also in Line 1, we are checking whether there is a value for the `modifier` key in JSON.  If there is, we are passing it to the title as a CSS class.  If no value is provided nothing will be added.
* In line 2, we check whether a URL was provided in the JSON file, and if so, we wrap the `{{ title }}` variable in a `<a>` tag to turn the title into a link.  The **href** value for the link is `{{ url }}`.  If no URL is provided in the JSON file, we simply print the value of `{{ title }}`as plain text.

### Compiling the code

If Pattern Lab is running you should see the updates to the title component.  Otherwise run the commands below:

```bash
npm run watch
```

### Just for fun 💥

* Try changing the title level in `yml` to anything other than H2.
* Inspect your code to see your changes to the title pattern.

**Congratulations!** You just built your first reusable component! 🙌 🎉
