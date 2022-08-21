# Vue Components and Props

![](https://miro.medium.com/max/3840/1*nfvapd86apvGH-hNBYkYuw.png)

## Getting Started

- Fork and Clone
- `npm install`
- `npm run serve`

## Overview

In this lesson, we'll cover how to setup and utilize Vue components and how to pass `props` to those components. Because Vue is an `opinionated` framework, there are a few rules that we must follow in order for our components to play nice.

## Creating a component

Let's start by creating a new components folder in our `src` directory:

```sh
mkdir src/components
```

Next we'll create a `MyComponent.vue` file. The name here means nothing, however it is important to note when creating a `Vue` component we must use the `.vue` file extension.

### Component Structure

In the world of Vue, components are structured utilizing 3 tags/elements,

- `<template>`
- `<script>`
- `<styles>`

Below you'll find a table that tells you which tags are **required** in a vue component:

| Tag Name   | Required |
| ---------- | -------- |
| `template` | &#9745;  |
| `script`   | &#9745;  |
| `styles`   | &#9744;  |

### Tag Breakdown

---

### Template

The `template` tag is one of the most important, this tag will contain all of our `jsx` for our vue component. The `template` is a skeleton of what our `component` should look like. It will give us the ability to display:

- dynamic values (state/props)
- event listeners (click/change)
- conditional rendering
- multiple components with loops

The `template` tag supports 2 different ways of writing our jsx:

- `pug`
- `html`

We'll be using the `html` templating style for this course.

### Script

The `script` tag is where all of our javascript will be written. The script tag will/can contain the following:

- state
- component imports
- prop declarations/typings
- component lifecycle methods
- component methods

The script tag has a couple of ways that it can be written:

- typescript
- `Vue Composition Api`
- ES6 Javascript

We'll be using the `ES6 Javascript` script templating.

### Styles

The style tag is an interesting one. This tag is **not** required in order for our application to function, but gives us some neat abilities and css preprocessor support. The style tag can be used in the following ways:

- CSS3
- Scoped css, localizes the styles to the component where the styles are written.
- SCSS
- LESS

If writing your styles with your components makes your life harder, you can go the simpler way and create a css file within `src` and import the file into your component. :grinning:

---

## Writing our first Vue component

Open the `MyComponent.vue` file in your editor.

It's going to start blank, but by the time we're done we'll have something rendering to our page.

### Templating

Let's start with setting up a template for our component:

```jsx
<template>
  <div>
    <h3>My Component</h3>
  </div>
</template>
```

A few important notes about templates:

- It must return a `jsx` element, the `template` tag **DOES NOT COUNT**.
- The returned element should be a `block` element such as:
  - `div`
  - `main`
  - `section`
- Inline elements are not recommended, these include:
  - `span`
  - `img`
  - `a`

### Scripts

Next we'll set up our `script`

**Below** the `template`, add in a script tag:

```jsx
<script></script>
```

Our `script` tag will contain a few things:

- a name for our component (Yes we get to name components, and no `Fido` is not acceptable)
- imports, components, styles, helper functions etc.
- a list of components available to the current component
- Any props that we want this component to accept, (yes, we have to tell our component what props it's going to see)
- `data` which is another term for `state`
- methods available to our component
- lifecycle methods/hooks

It's quite a bit I know, but we won't always use _everything_... except a few things. Here's a list of required properties:

- `name`

That's it, the only thing that's actually required in order for our component to work.

Let's set up our `script` for our component. Inside of the `script` tag, add in the following:

```jsx
<script>
export default {
    name: 'MyComponent'
}
</script>
```

Notice the syntax here, the script tag must always export an object. Hence why we're using `export default {}`.

### Styles

Finally underneath our `script`, we'll add a `style` tag. We won't be doing anything too fancy, but you're free to tinker and experiment.

```jsx
<style>
    h3 {
        color: #80cbc4;
    }
</style>
```

## Templating Order

Here's a quick reference on what order Vue components should be set up:

```jsx
<template>
  <!- Some JSX ->
</template>

<script>
// Any Imports
export default {
name: 'YourComponentName'
}
</script>

<style>
/* Some Styles */
</style>
```

## Importing and Utilizing Components

Now that we've set up our first component, let's import it into `App.vue`.

In `App.vue`, find the `components` object in the `script` tag and add in the following:

```jsx
<script>
import MyComponent from './components/MyComponent'
export default {
    name: 'App',
    components: {
        MyComponent
    }
}
</script>
```

Notice here, we're using this `components` object and passing in our component. This is how `Vue` components keep track of what should be used where.

Let's take a look at our browser...

You should see the following error:

![component error](https://i.imgur.com/rY0NPcr.jpg)

What is this error and what does it mean? This is not specifically a `Vue` error, but a linting error.The linting built into Vue is very aggressive. Here's how that effects our project:

- No unsued variables are allowed
- No unused components are allowed

This error occurred because we told `App.vue` that we were going to use `MyComponent` but never did. So let's fix this. In the `template` of `App.vue`, add in `MyComponent`:

```jsx
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <MyComponent />
  </div>
</template>
```

There are two ways we can add components in our jsx:

- `<MyComponent/>`
- `<my-component/>`

Both can be used with Vue, but the PascalCased version is recommended. (It'll make life easier to differentiate between components and elements.)

Let's check our browser again and you should see the component being rendered.

![](https://sei-r.s3.amazonaws.com/u4_vue_components_props/component-render.png)

## Passing and Registering Props

Our component is now being rendered, which means, we can get to the fun stuff. Static components are all great, but they'd be much better if they were dynamic. This is where `props` come in. Most frameworks utilize this concept of `passing` props and Vue is no different.

Props are:

- read only
- passed **down** to child components

### Registering Props

In `MyComponent.vue`, we'll see a couple of different ways to declare and register props. Let's start with the following:

```jsx
<script>
export default {
  name: 'MyComponent',
  props: {
    msg: String
  }
}
</script>
```

In this example, we're declaring that `MyComponent` will recieve a prop called `msg` and it is going to be a type of `String`. With Vue, we can define the datatypes of props that our component will recieve. We can take it a step further and even make them required as well:

```jsx
<script>
export default {
  name: 'MyComponent',
  props: {
    msg: {
      type: String,
      required: true
    }
  }
}
</script>
```

The above will not emit an error in the server, but will emit a warning in your console:

![prop-required](https://i.imgur.com/syfKnRF.jpg)

Another way of declaring props, is to use an array of the expected prop names:

```jsx
<script>
export default {
  name: 'MyComponent',
  props: ['msg']
}
</script>
```

With the above example, we lose type safety, but it is a much simpler way of declaring which props this component should expect.

We'll use the type safe example for this exercise:

```jsx
<script>
export default {
  name: 'MyComponent',
  props: {
    msg: String
  }
}
</script>
```

### Rendering Props

Now that we've declared what props to expect in `MyComponent`, we can display that information on the ui. Find the `template` tag and replace the content inside of `<h3></h3>` with the following:

```jsx
<h3>{{ msg }}</h3>
```

Notice the syntax here, inside of the `template` dynamic values/variables are displayed with a double set of `{{}}`. A single set will not work.

Now that our `msg` prop is set up in our ui, let's show a new message. In `App.vue`, modify the following in your `template`:

```jsx
<MyComponent msg="This is my component!" />
```

You should see the following rendered on your page:

![msg-prop](https://i.imgur.com/rr5ehMe.jpg)

The above example maps the `msg` attribute to an object key and the value to whatever comes after `=`. The Vue engine then parses that information and forwards it to our component!

## You Do

Now that we've learned the basics of props and components, it's time to practice and build up the muscle memory:

- Create 2 more components
- One component must use the type safe syntax for props
- One component must use the array syntax for props
- Import and use both of them in `App.vue`

You can put any kind of props you want in these components.

## Recap

In this lesson, we learned how to:

- Create a component
- Set up the template for a component
- Pass and render props

## Resources

- [Component Registration](https://vuejs.org/v2/guide/components-registration.html)
- [Props](https://vuejs.org/v2/guide/components-props.html)
