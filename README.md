# Tailwind CSS - Button Components

This is a blog post/tutorial for creating button components using Tailwind CSS. As a bonus we'll leverage some modern tools like Vite and Tailwind's new JIT feature which makes local developement with Tailwind CSS blazing fast.

### Getting started

Vite makes scaffolding a new project pretty seamless. For the purposes of this guide I'll leverage a basic Vue.js app by passing the vue template during project creation. You can name your project whatever you wish.

```bash
yarn create @vitejs/app tailwindjit-tour --template vue
```

This should go fetch basic dependencies and create a new folder with a set of folders and files inside. The general idea is that you'll work inside the `src` folder and everything builds to a `dist` folder which will contain all static assets.

Since we are wanting to leverage Tailwind CSS we need to install it as well. Tailwind depends on `autoprefixer` so here's the one-liner to get things added:

```
yarn add @tailwindcss/jit tailwindcss@latest postcss@latest autoprefixer@latest -D
```

After this installs you might notice the `package.json` file updates with the dependencies we'll need:

```json
{
  "name": "tailwindjit-tour",
  "version": "0.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "serve": "vite preview"
  },
  "dependencies": {
    "vue": "^3.0.5"
  },
  "devDependencies": {
    "@tailwindcss/jit": "^0.1.18",
    "@vitejs/plugin-vue": "^1.1.5",
    "@vue/compiler-sfc": "^3.0.5",
    "autoprefixer": "^10.2.5",
    "postcss": "^8.2.9",
    "tailwindcss": "^2.0.4",
    "vite": "^2.1.3"
  }
}
```

### Tailwind CSS Configuration

Tailwind depends on `postcss` which is a package we just installed. PostCSS allows you to pass some configuration to it based on a file called `postcss.config.js`. Create that file and store it at the root of your new project.

Inside of it we'll need the following:

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    '@tailwindcss/jit': {},
    autoprefixer: {},
  },
}
```

This code is telling PostCSS to use the `@tailwindcss/jit` package as a source of truth for CSS along side the `autoprefixer` package we installed.


Finally, we need a Tailwind configuration file similar to the `postcss.config.js` file.

Tailwind ships with a command line utility for generating this fairly easily.

```bash
npx tailwind init

# tailwindcss 2.0.4
# ✅ Created Tailwind config file: tailwind.config.js
```
_I'm using Tailwind 2.0.4_


And to round out our Tailwind installation we need a CSS file with the `@tailwind` imports inside. I'll create a file called `tailwind.css` and add those.


```css
/* src/tailwind.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

This file then needs to be imported inside the `main.js` file inside our `src` folder.

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import './tailwind.css' // Add this line

createApp(App).mount('#app')
```

If your server isn't running you can fire it back up by running:

```bash
yarn dev
```

### Configuring the project

Since Vite ships with a `HelloWorld.vue` component example I've modified it to relate more to our project.

- `src/components/HelloWorld.vue` becomes `src/components/TailwindButtons.vue`.

The `App.vue` single-file component file contains the following:

```vue
<template>
  <div class="container mx-auto px-6 py-12">
    <TailwindButtons />
  </div>
</template>

<script setup>
import TailwindButtons from './components/TailwindButtons.vue'
</script>
```

Note: A cool feature of Vue 3 here is not having to declare components explicitly. Super neat if you're coming from Vue 2.


The `TailwindButtons.vue` component is where our work will be done. Here's where I ended up:

```vue
<!-- src/components/TailwindButtons.vue -->
<template>
  <SolidButtons />

  <hr class="my-16" />

  <OutlinedButtons />

  <hr class="my-16" />

  <IconButtons />

  <hr class="my-16" />

  <GroupedButtons />

  <hr class="my-16" />

  <DropdownButtons />
</template>

<script setup>
import SolidButtons from "../components/SolidButtons.vue"
import OutlinedButtons from "../components/OutlinedButtons.vue"
import IconButtons from "../components/IconButtons.vue"
import GroupedButtons from "../components/GroupedButtons.vue"
import DropdownButtons from "../components/DropdownButtons.vue"
</script>
```

Because buttons are fairly repetative UI I chose to extract Tailwind's classes for each variant to my own custom component-based classes. That ends up looking like the following:

```css
/* src/tailwind.css */
@tailwind base;
@tailwind components;

.btn {
  @apply px-5 py-3 shadow-sm transition ease-in-out duration-300 rounded leading-snug whitespace-nowrap text-base font-semibold;
}

.btn.btn-sm {
  @apply px-4 py-2 text-sm;
}

.btn.btn-lg {
  @apply text-lg px-8 py-4;
}

.btn-primary {
  @apply text-white bg-blue-500 hover:bg-blue-600;
}

.btn-primary.btn-outline {
  @apply text-blue-600 border border-blue-600 bg-transparent hover:bg-blue-600 hover:text-white;
}

.btn-secondary {
  @apply text-white bg-indigo-500 hover:bg-indigo-600;
}

.btn-secondary.btn-outline {
  @apply text-indigo-600 border border-indigo-600 bg-transparent hover:bg-indigo-600 hover:text-white;
}

.btn-tertiary {
  @apply text-white bg-gray-600 hover:bg-gray-700;
}

.btn-tertiary.btn-outline {
  @apply text-gray-600 border border-gray-600 bg-transparent hover:bg-gray-600 hover:text-white;
}

@tailwind utilities;


```


Then each component has the following:

```vue
<!-- src/components/SolidButtons.vue -->
<template>
  <h2 class="font-black text-3xl text-gray-900 mb-2">Solid</h2>
  <h3 class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2">
    Small
  </h3>

  <div class="mb-6">
    <button class="btn btn-primary btn-sm mr-4">Primary</button>
    <button class="btn btn-secondary btn-sm mr-4">Secondary</button>
    <button class="btn btn-tertiary btn-sm">Tertiary</button>
  </div>

  <div class="mb-6">
    <h3
      class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2"
    >
      Default
    </h3>

    <button class="btn btn-primary mr-4">Primary</button>
    <button class="btn btn-secondary mr-4">Secondary</button>
    <button class="btn btn-tertiary">Tertiary</button>
  </div>

  <h3 class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2">
    Large
  </h3>

  <button class="btn btn-primary btn-lg mr-4">Primary</button>
  <button class="btn btn-secondary btn-lg mr-4">Secondary</button>
  <button class="btn btn-tertiary btn-lg">Tertiary</button>
</template>
```

```vue
<!-- src/components/OutlinedButtons.vue -->
<template>
  <h2 class="font-black text-3xl text-gray-900 mb-2">Outline</h2>

  <div class="mb-6">
    <h3
      class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2"
    >
      Small
    </h3>
    <button class="btn btn-primary btn-sm btn-outline mr-4">Primary</button>
    <button class="btn btn-secondary btn-sm btn-outline mr-4">Secondary</button>
    <button class="btn btn-tertiary btn-sm btn-outline mr-4">Tertiary</button>
  </div>

  <div class="mb-6">
    <h3
      class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2"
    >
      Default
    </h3>
    <button class="btn btn-primary btn-outline mr-4">Primary</button>
    <button class="btn btn-secondary btn-outline mr-4">Secondary</button>
    <button class="btn btn-tertiary btn-outline mr-4">Tertiary</button>
  </div>

  <div class="mb-6">
    <h3
      class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2"
    >
      Large
    </h3>
    <button class="btn btn-primary btn-lg btn-outline mr-4">Primary</button>
    <button class="btn btn-secondary btn-lg btn-outline mr-4">Secondary</button>
    <button class="btn btn-tertiary btn-lg btn-outline mr-4">Tertiary</button>
  </div>
</template>
```


```vue
<!-- src/components/IconButtons.vue -->
<template>
  <h2 class="font-black text-3xl text-gray-900 mb-2">Icons</h2>

  <div class="mb-6">
    <h2
      class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2"
    >
      Small
    </h2>

    <button class="btn btn-sm btn-primary group mr-4">
      <IconStar
        class="w-5 h-5 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Primary
    </button>
    <button class="btn btn-sm btn-secondary group mr-4">
      <IconStar
        class="w-5 h-5 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Secondary
    </button>
    <button class="btn btn-sm btn-tertiary group">
      <IconStar
        class="w-5 h-5 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Tertiary
    </button>
  </div>

  <div class="mb-6">
    <h2
      class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2"
    >
      Default
    </h2>

    <button class="btn btn-primary group mr-4">
      <IconStar
        class="w-6 h-6 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Primary
    </button>
    <button class="btn btn-secondary group mr-4">
      <IconStar
        class="w-6 h-6 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Secondary
    </button>
    <button class="btn btn-tertiary group">
      <IconStar
        class="w-6 h-6 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Tertiary
    </button>
  </div>

  <div class="mb-6">
    <h2
      class="uppercase text-sm font-semibold tracking-wider text-gray-700 mb-2"
    >
      Large
    </h2>

    <button class="btn btn-primary btn-lg group mr-4">
      <IconStar
        class="w-8 h-8 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Primary
    </button>
    <button class="btn btn-secondary btn-lg group mr-4">
      <IconStar
        class="w-8 h-8 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Secondary
    </button>
    <button class="btn btn-tertiary btn-lg group">
      <IconStar
        class="w-8 h-8 stroke-current text-white inline-block mr-1 group-hover:opacity-70"
      />
      Tertiary
    </button>
  </div>
</template>

<script setup>
import IconStar from "../components/IconStar.vue"
</script>
```

```vue
<!-- src/components/GroupedButtons.vue -->
<template>
  <h2 class="font-black text-3xl text-gray-900 mb-2">Grouped</h2>

  <div class="flex items-center">
    <button
      class="btn border-l rounded-r-none border-b border-t rounded-l hover:bg-gray-100"
    >
      One
    </button>
    <button class="btn border rounded-none hover:bg-gray-100">Two</button>
    <button
      class="btn border-t border-r border-b rounded-l-none rounded-r hover:bg-gray-100"
    >
      Three
    </button>
  </div>
</template>
```
```vue
<!-- src/components/DropdownButtons.vue -->
<template>
  <h2 class="font-black text-3xl text-gray-900 mb-4">Dropdowns</h2>
  <button
    class="btn btn-primary flex items-center justify-between pr-3"
    @click.prevent="active = !active"
  >
    Dropdown
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="20"
      height="20"
      viewBox="0 0 20 20"
      fill="none"
      class="w-5 h-5 text-white fill-current ml-2 transform transition duration-200"
      :class="{ 'rotate-180': active }"
    >
      <title>chevron-down</title>

      <path
        fill-rule="evenodd"
        clip-rule="evenodd"
        d="M5.293 7.293a1 1 0 0 1 1.414 0L10 10.586l3.293-3.293a1 1 0 1 1 1.414 1.414l-4 4a1 1 0 0 1-1.414 0l-4-4a1 1 0 0 1 0-1.414z"
      ></path>
    </svg>
  </button>

  <ul
    v-if="active"
    class="list-reset bg-white border p-4 rounded-b-lg shadow-xl w-64"
  >
    <li>
      <a href="#" class="px-3 py-2 hover:bg-gray-100 rounded block mb-1"
        >Item 1</a
      >
    </li>
    <li>
      <a href="#" class="px-3 py-2 hover:bg-gray-100 rounded block mb-1"
        >Item 2</a
      >
    </li>
    <li>
      <a href="#" class="px-3 py-2 hover:bg-gray-100 rounded block mb-1"
        >Item 3</a
      >
    </li>
  </ul>
</template>

<script>

export default {
  data() {
    return {
      active: false
    }
  }
}

</script>
```
