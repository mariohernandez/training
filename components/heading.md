# Heading Component

Following the [Atomic Design ](https://bradfrost.com/blog/post/atomic-web-design/)methodology we are going to build a simple component or pattern.  The Heading pattern is an atom which prints a string of text as the title for a page, paragraph, or other component.

As we saw in the [Component Architecture](essentials/untitled-3.md) page, most components will need the following files:

| File type | Purpose |
| :--- | :--- |
| `.twig` | Component's HTML and Twig logic |
| `.scss` | Component's styles |
| `.json` or `.yml` | Component's stock content |

Some components may also include:

| File type | Purpose |
| :--- | :--- |
| `.js` | Component's interactive behavior |
| `.md` | Component's annotations or specs details |

### Building the component

#### Component's stock content

Let's start by first identifying the content for the component.   Since this is a title field, we only need a string of text.  We'll dive into more complex components in future exercises.

{% hint style="info" %}
**NOTE:**  All components will be created inside `src/patterns/components`.

On a typical Drupal project the full path may look something like this: `<project-root>/web/themes/custom/<your-theme-name>/src/patterns/components/`
{% endhint %}

1. Inside _components_ create a new directory called **heading**
2. Inside the _heading_ directory create a new file called **heading.json**
3. Inside _heading.json_ add the following code:

```yaml
{
  "title": "Welcome to the best training workshop!"
}
```

We just created key/value pair for the heading with a key of **title** and **value** of _Welcome to the best training workshop!_.

#### Component's Markup

Now let's write some HTML to be able to see the Heading component in the browser.

1. Inside the _heading_ directory create a new file called **heading.twig**
2. Inside `heading.twig` add the following code:

```php
<h1 class="heading">{{ title }}</h1>
```

We created a **h1** heading in which we pass the value of title from the `json` file.

#### Component's styles

We don't need to write any CSS for this component, but let's at least create a Sass file for when we need to write styles.

1. Inside the _heading_ directory create a new file called **heading.scss**
2. Inside `heading.scss` add this code:

```css
// Import site utilities
@import '../../global/utils/init';
```

The code above simply imports global utilities from our theme which will be needed as we start writing styles in Sass.  More on this later.

### Compiling the code

Now that the Heading component is done, let's compile the code so we can see it in Pattern Lab.

While in your theme's root directory, run the following commands in your command line and press **Return**

`npm run build`

`npm run watch`

The **build** command above compiles all scss,  twig and js. files, and should build the new Heading component in Pattern Lab.  The **watch** command watches for changes to your code and automatically compiles them. This is great so you don't have to keep compiling your code every time.

At the bottom of the watch command you will notice a list of URLs.  In your browser of choice open the following url: [http://localhost:3000](http://localhost:3000).  This will open Pattern Lab where you can find the Heading pattern under components.

### Improving the Heading component

The heading component looks good and it will work great as long as we always want to use a H1. However, the component is pretty static and it does not offer much flexibility. What if we wanted to use a h2 or h3? or what if the title field is a link to a full page? Then the heading component would probably not work because we have no way of changing the heading level from h1 to any other level or add a URL . to it. Let's re-work the heading component so we make it more dynamic.

* Update `heading.json` to look like this:

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

We just created an object for the heading with key/value **heading\_level, modifier, title**, and **url**.

* The **heading\_level** is something we will use later as we start nesting the heading component into other components. This will allows us to change the headings from say h1 to h2 if we need to.
* The **modifier** key allows us to pass a modifier CSS class when we make use of this component. The modifier class will make it possible for us to style the heading differently if needed.
* the **title** key is the title's sring of text that will become the title of a page or a component.
* ... and finally, the **url** key, if present, will allow us to wrap the title in an `<a>` tag, to make it a link.

### Update the heading's markup and logic

* Update the `heading.twig` file to look like this:

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

Let's break things down to explain what's happening here since the twig code has significantly changed:

* Line 1 makes use of `heading.heading_level` to complete the number part of the heading.  If a value is not provided for `heading_level` in the JSON file, we are setting a default of `2`.  This will ensue that by default we will have a `<h2>` as the title, much better than `<h1>` as we had before.  This value can be changed per use case if needed.  Line 9 closes the heading tag.
* On line 2 we check whether a url was provided in the JSON file, and if so, we wrap the `{{ title }}` variable in a `<a>` tag to turn the title into a link.  The **href** value for the link is `{{ heading.url }}`.  If no url is provided in the JSON file, we simply print the value of `{{ title }}`as plain text.
* As part of the `class` attribute in line 1, we check whether there is a value for the modifier key, if there is we pass it as an additional css class to the already available `heading` class.

#### Compiling the code

Repeat steps above for compiling code or if you have the watch task running, your Pattern Lab page should had automatically reloaded with the new changes.

**Just for fun 💥**

* Try changing the heading level in `heading.json` to anything other than H2 and compile the code.
* Inspect your code to see your changes to the Heading pattern.
