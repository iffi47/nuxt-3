<script setup>
const query = ref("");
let movies= ref([]);
// const apiKey = import.meta.env.OMDB_API_KEY;
const searchMovie = async (e) => {
  e.preventDefault();
  if (!query.value) return;

  const data = await $fetch(
    `http://www.omdbapi.com/?s=${query.value}&apikey=499650a`
  );
  if(data && data.Search){
    movies.value = data.Search;
  }
};
</script>

<template>
  <div>
    <form>
      <input class="movie_search" type="text" placeholder="Search Movies..." v-model="query" />
      <button class="button" @click="searchMovie" type="submit">Search</button>
    </form>
    <ul style="display: flex; flex-wrap: wrap; gap: 20px; list-style: none; padding: 0; margin-top: 20px;">
      <li v-for="movie in movies" :key="movie.imdbID" style="border: 1px solid #ccc; border-radius: 8px; padding: 10px; width: 200px; text-align: center;">
        <nuxt-link :to="{name: 'movies-id', params: {id: movie.imdbID}}">
        <img :src="movie.Poster" alt="Movie Poster" style="width: 100%; height: auto; border-radius: 4px;" />
        </nuxt-link>
        <h3>{{ movie.Title }}</h3>
        <p>{{ movie.Year }}</p>
      </li>

    </ul>
  </div>
</template>

<style scoped>

.movie_search {
  padding: 10px;
  font-size: 16px;
  width: 250px;
  border: 1px solid #ccc;
  border-radius: 4px;
};

.button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
};
</style>
