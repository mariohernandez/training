# Integrating Featured Content

![Card Wide variant](../.gitbook/assets/card-wide.png)

In the previous exercise we used the default card component to display blog posts that are part of the **From our blog** section.  In this exercise, you will use the **Card Wide** variant to style blog posts that are part of the **Featured Content** section.  The process for achieving this is exactly as we did with the regular card in the previous exercise.  Here are some things to note:

* In the previous exercise we used the **Teaser** view mode to create a custom twig template.  In this exercise use the **Featured** view mode
* In order to achieve the Card Wide look, we need to pass a modifier class of `card--wide` when the component is integrated
* The card wide does not use `tags`, but it does use the `author` field
* Use the appropriate twig block for displaying the date, in **short** format.  Remember, we created two twig blocks in the card component to determine where the date will be displayed depending on the card we are working with.
* The card wide uses the `short` date format we updated in the previous exercise
* Finally, the template suggestion you will need to create is `node--blog--featured.html.twig`

\`\`

