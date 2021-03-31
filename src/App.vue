<template>
  <div class="container mx-auto px-6 pb-32 pt-10">
    <div class="mb-20 text-center">
      <a href="https://web-crunch.com/" target="_blank">
        <img
          src="https://pbs.twimg.com/profile_images/1364406200734003202/GZZEdK15_400x400.jpg"
          class="w-16 h-16 rounded-full mx-auto mb-4"
        />
      </a>
      <h1
        class="text-3xl lg:text-6xl font-black text-transparent bg-clip-text bg-gradient-to-r from-green-500 to-blue-500 via-indigo-600 mb-4"
      >
        Tailwind CSS Button Components
      </h1>
      <p class="text-gray-500 text-lg italic">
        See more at
        <a href="https://web-crunch.com/" target="_blank" class="underline"
          >web-crunch.com</a
        >
      </p>
    </div>
    <TailwindButtons />
  </div>
</template>

<script setup>
import TailwindButtons from './components/TailwindButtons.vue'
</script>
