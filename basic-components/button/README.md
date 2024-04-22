# Button component

Buttons are some of those things that are used over and over on a website. For this reason it makes sense to create a new component for it.

## Requirements for the Button component

* Be able to use either an **`<a>`** or **`<button>`** element when using the button component
* Ability to create button variations based on modifier class

## Exercise 2: Building the Button component

### Data structure

1. Inside the **components/01-atoms** directory create a new directory called **button**
2. Inside the **button** directory create a new file called **button.yml**
3. Inside **button.yml** add the following:

```yml
---
modifier: ''
text: 'Visit our website'
url: ''
```

The data structure above is as simple as it gets.

* The **modifier** key will allow us to add a modifier CSS class to the component so we can create variations.
* The **text** key will print the button's label
* The **url** will be used as the link's href value to create a link that looks like a button.

## Markup and logic

Before we start, let's review one of the requirements which calls for using an `<a>` or a `<button>` HTML element. The question is, how can we determine when to use one or the other?
An easy way is by using the **url** key as the validator. For example, if the **url** key has a value, meaning a URL of some sort, this tells us that the intention is for the button to take the visitors to a website, a webpage or a section within the page we are reading. If this is true, then we know we need to use an `<a>` element. Whereas if the **url** key is empty, we don't need a link, we need an actual button element to perform an action like submit a form, toggle a switch, expand a panel, etc. So let's write the markup with this logic in mind.

* Inside the **button** directory, create a new file called **button.twig**
* Inside **button.twig** add the following:

```php
{% if url %}
  <a href="{{ url }}" class="button{{ modifier ? ' ' ~ modifier }}">
    {{ text }}
  </a>
  {% else %}
  <button class="button{{ modifier ? ' ' ~ modifier }}">
    {{ text }}
  </button>
{% endif %}
```

In the code above we are simply checking if the URL is empty or not. If it has a value, we wrap the value of the **text** key in a link, otherwise we use the **button** element. Simple.

## Styles

1. Inside the **button** directory create a new file called **button.css**
2. Inside **button.scss** add the following:

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

## Button story

As we did with the Title component, we are going to create a story for the Button component.

* Inside the **button** directory create a new file called **button.stories.jsx**
* Inside **button.stories.jsx** add the following:

```js
import parse from 'html-react-parser';

import button from './button.twig';
import data from './button.yml';
import './button.css';

const settings = {
  title: 'Atoms/Button',
};

// Default button story.
export const Button = {
  render: (args) => parse(button(args)),
  args: { ...data },
};

/** Primary button story */
export const Primary = {
  ...Button,
  name: 'Primary button',
  args: {
    ...Button.args,
    modifier: 'button--primary',
};

/** Secondary button story */
export const Primary = {
  ...Button,
  name: 'Secondary button',
  args: {
    ...Button.args,
    modifier: 'button--secondary',
};

export default settings;
```

So we have created a story for the Button, but in addition, we also created two additional stories that represent different button states. The **Primary button** is intended to be used as the main button througout the site, where as the **Secondary button** can be used as a more subtle version of the button. You can see this if you run:

```bash
npm run storybook
```
