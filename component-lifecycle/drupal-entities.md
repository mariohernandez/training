# Drupal entities

### Whose line is it anyway?

Before embarking on this Drupal journey, keep in mind that your role in this process may vary.  Depending on your team, your skillset or other factors, you may not be responsible for building the front-end and back-end of a project.  For example, a typical project for me consists of an architect building all of Drupal's infrastructure, me, as a front-end developer building components in Pattern Lab, and perhaps a back-end developer integrating the components with Drupal.  However, in other projects I may be responsible for building and integrating components.

### Drupal entities

Typically in a component-based project, Drupal will use entities to build the components infrastructure in the back end.  Entities such as content types, blocks, paragraph types, and even views, are some of the ways we can transition from a traditional development approach of building pages to a modular system of components.

### Entity references

In our project, we have a large collection of movies.  It would be nice to be able to pick any movie and turn its image into the hero for our homepage.  Even better, it would be nice to be able to change the homepage hero to any movie at will.  Well, we can do this by using an entity reference field for our hero in the Homepage content type.  An entity reference field in combination with view mode display will allow us to achieve all of this.

Before we can add a Hero to the homepage, let's first build a new content type for the homepage.
