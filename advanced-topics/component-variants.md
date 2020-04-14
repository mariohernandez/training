# Component Variants

Variants are useful when you have one component that has **multiple different possible implementations**. These could be implemented as separate components but often it's easier and more semantic to create them as variants of an existing component.

Let's take a look at the Card component for example. Here are two different ways in which this component will be displayed:

![Default Card component](../.gitbook/assets/card.png)

![Example of Card variant](../.gitbook/assets/card-wide.png)

## Planning for component variants

Looking at the two cards above, we see that they are practically the same card component but with changes for each variant. There are many factors that determine if a component could be used as the base for variants.

* Does the proposed variant have the overall look and feel of the original component?
* Are there common patterns \(fields, markup, layout, etc.\) that can facilitate a variant vs. a whole new component?
* Does the component behavior and layout lend themselves to new variants without altering markup or sacrificing accessibility or user experience?
* Can I achieve the variants with a CSS Modifier class or Twig blocks?

These are questions you should ask yourself before deciding to create component variants. Although technically there are ways a component variant can be created, this does not mean you should. If not properly planned, you could paint yourself in a corner when your components have been over engineered in an effort to accommodate for variants. I would much rather build separate components and make the integration easy, than trying to build over complicated variants that will present issues in the long run with integration or implementation.

In the next page we will dive deeper into effectively creating the Card variants we see above.

