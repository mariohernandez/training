# Front-end setup

The first part of this training focuses on getting the front-end environment setup as well as building components in Storybook, later in the training we will start interacting with Drupal to make use of the Storybook components within Drupal.

## Building the front-end project

To start we need to build a [ViteJS App](https://vitejs.dev/guide/){target=_blank rel=noopener} which will serve as the foundation of our front-end environment.

**Important**: You need **NodeJS 18+ or 20+** ([See releases](https://nodejs.org/en/download){target=_blank rel=noopener}).

### ViteJS

1. Anywhere in your computer, create a new directory called **storybook**
1. In your command line, navigate into the newly created **storybook** directory and run the following commands:

```bash
npm create vite@latest . -- --template react
npm install
npm run dev
```

**Note**: _You could use any name for your project but this training uses **storybook** in all the exercises_.

After running npm run dev above, you will be prompted with a local URL which will open to a basic Vite/React app.

### Storybook

With the Vite app now in place, we can proceed to integrating [Storybook](https://storybook.js.org/docs/get-started) into it. Before proceeding, stop the Vite app, if it's running, by pressing **Ctrl + C**.

Still inside the **storybook** directory, run

```bash
npx storybook@latest init --type react
```

Upon completion of installing Storybook, a basic Storybook app should launch on your default browser. Storybook comes with a hand-ful of pre-built demo components.

#### Starting/Stopping Storybook on demand

Should you ever need to stop Storybook you can do so by pressing **Ctrl + C** on your keyboard. To restart Storybook run

```bash
npm run storybook
```

## Environment directory structure

Building an environment for a project is not usually something you do in one sitting. You may start with only the necesary pieces to get you started and build the rest as you go or as you need it. Before we can start building components, let's put the directory structure our environment will use.

As previously stated, we will use the Atomic Design naming convention for our directory structure. The only thing we will change is instead of naming a directory **templates**, we will name it **sections**. This will make it less confusing when we start working with Drupal because Drupal uses the name **templates** for storing custom twig template suggestions.

* Inside the **storybook** directory, create the following directory structure:

```twig
|--src
|  |--components/
|     |--01-atoms/
|     |--02-molecules/
|     |--03-organisms/
|     |--04-sections/
|     |--05-pages/
```

For now this will be good enough to start building components. Let's do that next.
