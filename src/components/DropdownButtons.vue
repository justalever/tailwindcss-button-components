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
