# Component Integration

### What is component integration?

At a high level, component integration means connecting Drupal to pre-built components from a design system such as Pattern Lab.  By default Drupal has no knowledge of any components in Pattern Lab, but with the use of the [Component Libraries](https://www.drupal.org/project/components) module and through the use of Presenter templates, we can wire components so they get rendered in Drupal, using Drupal data,.

### Twig debugging

Before we can begin integrating components we need to turn on Twig debugging in Drupal.  This will allow us to identify the right Drupal templates we need to work with to integrate the hero and other components.

&lt;add instructions to enable twig debugging&gt;

### Drupal entities

Typically in a component-based project, Drupal will use entities to build the components infrastructure in the back end.  Entities such as nodes, blocks, paragraph types, and even views, are some of the ways we can transition from a traditional development approach of building pages to a modular system of components.

Let's take the Hero component as an example, In Drupal we could build a custom block or a paragraph type called Hero.  This custom entity would be made of the same fields we identified when building the Hero component \(image, eyebrow, title, body, cta\). 

### Template suggestions

[Template suggestions](https://www.drupal.org/docs/8/theming/twig/working-with-twig-templates) are Twig templates used to override Drupal core or contrib modules templates. Template suggestions are saved in your theme's `/templates` directory. This is where Drupal knows to look for twig templates when rendering content. If it finds twig templates it uses those over the ones in core when rendering content.  Template suggestions are what we will use to integrate components with Drupal.  These template suggestions in the context of component integration, are typically referred to as **Presenter Templates** and as you will see, their only purpose is to pass data from Drupal to  the component.

#### Identifying template suggestions

If you have been using Drupal for a while you may be well familiar with where to get templates from or what to name them. However if you've never worked with template suggestion no worries, Twig debugging, which we enabled above, will help us identify the templates we need.

#### Do the following:

* In your Drupal site, create  a node where yoou can add a Hero, or visit a page that has a Hero
* Right-click anywhere on the hero and select **Inspect**  or **inspect element**, depending on your browser.  This will display the HMTL that makes up the page you are currently viewing.  See the screenshot below:

&lt;insert image here&gt;

If you look at the screenshot above, you will see a few things that are extremely helpful for creating the right template suggestions.

* The last line of the green text \(`BEGIN OUTPUT...`\) shows where the template being used by Drupal to render the Hero is located and what its name is.
* Just above that line, there is a list of files all of which begin with **node--**. This list is what we mean when we say _Template suggestions_.
* The file name with an **"x"** to the left of it is the template Drupal is currently using to render the Hero.

