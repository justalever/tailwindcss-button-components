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
