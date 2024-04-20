# Title Component

Following the [Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/) methodology we are going to build a simple component or pattern. The Title is an atom which prints a string of text as the title for a page, paragraph, or another component.

As we saw in the [Component Architecture](getting-started/component-architecture.md) page, most components will need the following files:

| File type         | Purpose                          |
| ----------------- | -------------------------------  |
| `.css`            | Component's styles               |
| `.twig`           | Component's HTML and Twig logic  |
| `.yml`            | Component's stock content        |
| `.stories.jsx`    | Storybook story                  |
| **Some components may also include**                 |
| `.js`     | Component's interactive behavior         |
| `.mdx`    | Component's annotations or specs details |

## Requirements for the Title component

* Able to print title in plain text or as a link
* Able to change heading level (h1, h2, h3, etc.)
* Able to accept a modifier class if needed

## Exercise 1: Building the Title component

### Data structure

Let's start by first identifying the variables we need for the component. This is a good time to start thinking how a title is created in Drupal. Since this is a title field, we only need a string of text, however, if we look at the requirements above, we see that we will need more than just a string of text.

1. Inside the **components/01-atoms** directory create a new folder called **title**
1. Inside the **title** folder create a new file called **title.yml**
1. Inside **title.yml** add the following code:

```yml
---
level: ''
modifier: ''
text: 'Component-driven development with Storybook!'
url: ''
```

In YAML or JSON files, data is structured using a **key/value** pair. Keys can be of any data type such as string, integer, array, object, etc.

### HTML or Markup

Now let's write some HTML to be able to see the title component in the browser.

1. Inside the ****title**** directory create a new file called **title.twig**
2. Inside **title.twig** add the following code:

```php
<h{{ level|default('2') }} class="title{{ modifier ? ' ' ~ modifier }}">
  {% if url %}
    <a href="{{ url }}" class="title__link">
      {{ text }}
    </a>
  {% else %}
    {{ text }}
  {% endif %}
</h{{ level|default('2') }}>
```

Wow! What's all this? 😮 Let's go over what all this code means and does.

* **level**: is a variable we can use to pass the value of the heading level we want (for example: 1, 2, 3 when paired with h woudl turn into h1, h2, h3, etc.)
* **modifier**: We are using a variable called modifier as a placeholder for when we need to pass additional CSS classes to the title.
* **text**: is the string of text that will be printed as a title
* **url**: As you can see, we have a condition that if an URL exists, we will wrap the text variable in an anchor tag so the title would print as a link. If no URL is present, then we would just print a plain text title.

As it is, the Title component satisfies all the requirements we established at the begining.

### Styles

We don't need to write any CSS as part of the component for two reasons:

1. Most titles are styled at a global level to inherit a consistent look/feel throughout your site,
1. In the event a title needs special styling, those styles are usually written in the component where the title is being used.

## Viewing in Storybook

In Storybook you will notice that the Title component we just built is nowhere to be found. This is because Storybook can only render a component if it's written in React and in a file with a name such as ***.stories.jsx**, where ***** is the name of the story.

### Storybook story

With the component now in place, we can proceed to creating the Storybook story so we are able to view it inside Storybook.

1. Inside the **title** directory create a new file called **title.stories.jsx**
1. Inside **title.stories.jsx** add the following:

```js
import parse from 'html-react-parser';

import title from './title.twig';
import data from './title.yml';

const component = {
  title: 'Atoms/Title',
};

// Plain text title story.
export const Title = {
  render: (args) => parse(title(args)),
  args: { ...data },
};

export default component;
```

* First we import the parser extension to be able to parse html into react
* Next we import Twig and YML files and assign a variable name to each
* In the **component** object we define the story name and its location
* Then we export the **Title** story in which we render everything from Twig while using variables from YML to pass as args.
* Finally, we export the default component.

### Launching Storybook

If Storybook is not running, run

```bash
npm run storybook
```

Now you should be able to see the Title story under the Atoms section in the sidebar.
