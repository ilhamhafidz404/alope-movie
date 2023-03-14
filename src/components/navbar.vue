<template>
  <nav
    class="flex justify-between items-center px-20 py-5 fixed top-0 left-0 right-0 z-40 dark:!text-white duration-500 dark:bg-[#181d23] text-black"
  >
    <div class="flex items-center">
      <img src="./../assets/logo.png" class="w-[50px] mr-3" />
      <h3 class="text-xl font-semibold">ALOPE MOVIE</h3>
    </div>
    <div class="flex items-center">
      <ul class="flex mr-10">
        <li class="mr-4">
          <a href="">Home</a>
        </li>
        <li class="mr-4">
          <a href="">Movie</a>
        </li>
        <li>
          <a href="">Series</a>
        </li>
      </ul>
      <button @click="toggleSearch()">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6 text-indigo-500"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
          />
        </svg>
      </button>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style>
</style>