<template>
  <section
    id="searchBox"
    class="fixed inset-0 bg-black/80 z-50 flex items-center justify-center hidden"
  >
    <button @click="toggleSearch()" class="absolute top-0 right-0 m-10">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M6 18L18 6M6 6l12 12"
        />
      </svg>
    </button>
    <div class="w-[900px]">
      <div>
        <div class="relative">
          <input
            type="text"
            v-model="search"
            class="w-full py-2 px-5 rounded"
          />
          <button
            @click="searchProcess()"
            class="absolute right-0 top-1/2 -translate-y-1/2 h-full bg-indigo-500 rounded-r px-5 text-white hover:bg-indigo-400"
          >
            Search
          </button>
        </div>
      </div>
      <div
        v-if="searchData != null"
        class="bg-white w-[900px] h-[500px] overflow-y-auto rounded mt-20"
      >
        <ul>
          <li
            v-for="result in searchData"
            :key="result.id"
            class="flex mb-3 p-4 rounded items-center"
          >
            <img
              :src="result.image"
              class="w-[100px] h-[150px] object-cover rounded-sm mr-3"
            />
            {{ result.title }}
          </li>
        </ul>
      </div>
    </div>
  </section>

  <nav
    class="flex justify-between items-center px-20 py-5 fixed top-0 left-0 right-0 z-40 text-white dark:!text-white duration-500 bg-white dark:bg-[#181d23]"
  >
    <div class="flex items-center">
      <img src="./assets/logo.png" class="w-[50px] mr-3" />
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
  <header
    class="w-full h-[800px] bg-cover text-white z-10 relative flex items-center before:content-[''] before:absolute before:inset-0 before:bg-black/50 before:z-[-1] pt-20"
  >
    <div class="container mx-auto flex justify-between items-center">
      <div>
        <h2 class="font-bold text-5xl">{{ topMovies.title }}</h2>
        <div class="flex items-center mt-4">
          <div class="mr-5 flex">
            <span
              class="border-2 border-white bg-white font-bold text-gray-800 px-3 mr-3"
            >
              {{ topMovies.contentRating }}
            </span>
            <span
              class="border-2 border-white font-bold text-gray-100 px-3 flex"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
                class="w-5 h-5 mr-1"
              >
                <path
                  fill-rule="evenodd"
                  d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
                  clip-rule="evenodd"
                />
              </svg>
              {{ topMovies.imDbRating }}
            </span>
          </div>
          <ul class="flex items-center">
            <li v-for="genre in topMovies.genreList" :key="genre" class="mr-3">
              <a href="">{{ genre.value }}</a>
            </li>
          </ul>
        </div>
        <p class="w-[800px] text-sm mt-5">{{ topMovies.plot }}</p>
      </div>
      <div>
        <img
          src="https://m.media-amazon.com/images/M/MV5BODZhNzlmOGItMWUyYS00Y2Q5LWFlNzMtM2I2NDFkM2ZkYmE1XkEyXkFqcGdeQXVyMTU5OTA4NTIz._V1_Ratio0.6716_AL_.jpg"
          alt="Ant Man - Quantumania Banner"
          class="w-[400px]"
        />
      </div>
    </div>
  </header>

  <main class="container mx-auto grid grid-cols-4 gap-14 mt-20">
    <div class="col-span-4 text-center">
      <span class="font-2xl block uppercase text-indigo-500"
        >Best TV Series</span
      >
      <h2 class="text-5xl font-bold dark:text-gray-100">
        World Best TV Series
      </h2>
    </div>
    <div
      v-for="movie in movies"
      :key="movie"
      class="mb-10 cursor-pointer relative after:content-[''] after:absolute after:bg-black/10 hover:after:inset-0 after:duration-500 after:scale-0 hover:after:-scale-100 after:rounded-md"
      @click="showFilm(movie.id)"
    >
      <img
        :src="movie.image"
        class="rounded-md w-full max-h-[450px] object-cover"
      />
      <div class="flex items-center mt-5 justify-between px-3">
        <h5 class="font-semibold w-[90%] dark:text-gray-100">
          {{ movie.title }}
        </h5>
        <span class="text-indigo-500 w-[10%]">2022</span>
      </div>
      <div class="flex justify-between mt-3 px-3 pb-3">
        <div>
          <span class="bg-indigo-500 text-white px-2 rounded font-semibold"
            >HDTV</span
          >
        </div>
        <div class="flex items-center text-sm dark:text-gray-100">
          <span class="flex items-center mr-3">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="currentColor"
              class="w-5 h-5 mr-1 text-indigo-500"
            >
              <path
                fill-rule="evenodd"
                d="M10 18a8 8 0 100-16 8 8 0 000 16zm.75-13a.75.75 0 00-1.5 0v5c0 .414.336.75.75.75h4a.75.75 0 000-1.5h-3.25V5z"
                clip-rule="evenodd"
              />
            </svg>
            120 min
          </span>
          <span class="flex items-center">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="currentColor"
              class="w-5 h-5 text-yellow-500 mr-1"
            >
              <path
                fill-rule="evenodd"
                d="M10.868 2.884c-.321-.772-1.415-.772-1.736 0l-1.83 4.401-4.753.381c-.833.067-1.171 1.107-.536 1.651l3.62 3.102-1.106 4.637c-.194.813.691 1.456 1.405 1.02L10 15.591l4.069 2.485c.713.436 1.598-.207 1.404-1.02l-1.106-4.637 3.62-3.102c.635-.544.297-1.584-.536-1.65l-4.752-.382-1.831-4.401z"
                clip-rule="evenodd"
              />
            </svg>
            8.9
          </span>
        </div>
      </div>
    </div>
  </main>

  <div
    class="fixed w-[50px] h-[50px] rounded-full bg-indigo-500 z-40 bottom-0 right-0 flex items-center justify-center m-5"
  >
    <button class="cursor-pointer" onclick="toggleDarkMode()">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="w-6 h-6 text-white"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M12 3v2.25m6.364.386l-1.591 1.591M21 12h-2.25m-.386 6.364l-1.591-1.591M12 18.75V21m-4.773-4.227l-1.591 1.591M5.25 12H3m4.227-4.773L5.636 5.636M15.75 12a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0z"
        />
      </svg>
    </button>
  </div>

  <footer>
    <div class="container mx-auto py-10 flex justify-between items-center">
      <div class="flex items-center">
        <img src="./assets/logo.png" class="w-[70px] mr-5" />
        <h2 class="text-2xl text-white font-semibold">ALOPE MOVIE</h2>
      </div>
      <div class="text-white">
        <ul class="flex">
          <li class="mr-5">
            <a href=""> HOME </a>
          </li>
          <li class="mr-5">
            <a href=""> MOVIE </a>
          </li>
          <li>
            <a href=""> SERIES </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="container mx-auto">
      <hr class="border-2 border-indigo-500" />
    </div>
    <div class="container mx-auto py-10 text-white">
      <div>
        <ul class="flex">
          <li class="mr-5">
            <a href="">FAQ</a>
          </li>
          <li class="mr-5">
            <a href="">HELP CENTER</a>
          </li>
          <li class="mr-5">
            <a href="">TERM OF USE</a>
          </li>
          <li class="mr-5">
            <a href="">PRIVACY</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="bg-[#171d21] py-5">
      <div class="container mx-auto text-white">
        <p>&copy; 2023 Code with ALOPE. All Rights Reserved</p>
      </div>
    </div>
  </footer>
</template>

<script>
import axios from "axios";
export default {
  setup() {
    window.addEventListener("scroll", () => {
      const nav = document.querySelector("nav");
      nav.classList.toggle("bg-white", window.scrollY > 0);
      nav.classList.toggle("!text-gray-800", window.scrollY > 0);
      nav.classList.toggle("shadow-md", window.scrollY > 0);
      nav.classList.toggle("!py-3", window.scrollY > 0);
      nav.classList.toggle("!px-10", window.scrollY > 0);
      nav.classList.toggle("dark:bg-[#181d23]", window.scrollY > 0);
    });
  },
  data() {
    return {
      movies: null,
      topMovies: null,
      search: null,

      searchData: null,
    };
  },
  mounted() {
    axios
      .get("https://imdb-api.com/en/API/BoxOffice/k_ye1jj0pg")
      .then((response) => {
        this.movies = response.data.items;
      });
  },
  created() {
    axios
      .get(
        "https://imdb-api.com/en/API/Title/k_ye1jj0pg/tt10954600/Images,Trailer,Ratings,"
      )
      .then((response) => {
        this.topMovies = response.data;
      });
  },
  methods: {
    showFilm(id) {
      const link = "https://imdb-api.com/en/API/Title/k_ye1jj0pg/" + id;
      window.open(link, "_blank");
    },

    searchProcess() {
      const link = "https://imdb-api.com/API/Search/k_ye1jj0pg/" + this.search;
      axios.get(link).then((response) => {
        this.searchData = response.data.results;
      });
    },

    toggleSearch() {
      const searchBox = document.querySelector("#searchBox");
      searchBox.classList.toggle("hidden");
    },
  },
};
</script>

<style>
header {
  background-image: url(https://m.media-amazon.com/images/M/MV5BYTU1NmYyMGUtYzA1ZS00YmYwLTgxYjYtZmM2OTUxYzNhMWI2XkEyXkFqcGdeQXVyODk4OTc3MTY@._V1_Ratio2.3800_AL_.jpg);
}
footer {
  background-image: url(https://codewithsadee.github.io/filmlane/assets/images/footer-bg.jpg);
}
</style>