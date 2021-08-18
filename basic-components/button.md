# Button Component

![](../.gitbook/assets/button.png)

Buttons are some of those things that are used over and over on a website. For this reason it makes sense to create a new component for it.

1. Inside _components_ create a new folder called **button**
2. Inside the _button_ folder create a new file called **button.json**
3. Inside _button.json_ add the following code:

{% tabs %}
{% tab title="button.json" %}
```yaml
{
  "button": {
    "text": "Hi, I'm a button",
    "url": "",
    "modifier": ""
  }
}
```
{% endtab %}
{% endtabs %}

We created an object called `button` and added several properties or attributes such as `text`, `url`, and `modifier`. By now we've seen this kind of data structure on other components.

## Writing the button's logic

1. Inside the _button_ folder create a new file called **button.twig**
2. Inside `button.twig` add the following code:

{% tabs %}
{% tab title="button.twig" %}
```php
{% if button.url %}
  <a href="{{ button.url }}" class="button{{ button.modifier ? ' ' ~ button.modifier }}">
    {{ button.text }}
  </a>
  {% else %}
  <button class="button{{ button.modifier ? ' ' ~ button.modifier }}">
    {{ button.text }}
  </button>
{% endif %}
```
{% endtab %}
{% endtabs %}

* We've added some logic to the button to ensure we render the right HTML element based on the data we receive. For example, if a URL is passed, we use an `<a>` tag with the class of **button**, otherwise we use a `<button>` tag. We always want to make sure we use proper semantic markup for accessibility and for the task at hand. An `<a>` tag will allow us to link to another page or a section within the same page, whereas a `<button>` element will allow us to perform an action such as submit content.

## Button Styles

1. Inside the `button` folder create a new file called **button.scss**
2. Inside `button.scss` add the following code:

{% tabs %}
{% tab title="button.scss" %}
```css
// Import site utilities
@import '../../global/utils/init';

.button {
  background-color: $color-navy-blue;
  border: 2px solid $color-navy-blue;
  color: $color-white;
  display: inline-block;
  line-height: 1.3;
  padding: 15px 40px;
  text-transform: uppercase;
  text-decoration: none;

  // Hover and focus states for base button
  &:hover,
  &:focus {
    color: $color-white;
  }

  // Styles for white button with gray outline.
  &.button--ghost {
    background-color: transparent;
    border: 2px solid $color-gray-dark;
    color: $color-gray-dark;
    padding: 8px 30px;

    // Hover and focus styles for ghost button.
    &:hover,
    &:focus {
      color: $color-gray-dark;
    }
  }
}
```
{% endtab %}
{% endtabs %}

* Some basic css styles to make our button look decent.  We can probably improve them but for now this will do.

## Compiling the code

Now that the Button component is done, let's compile the code so we can see it in Pattern Lab. If you already have Pattern Lab running you should see the new Button component. Otherwise, run the following command in your command line and press **Return**

```bash
npm run watch
```



