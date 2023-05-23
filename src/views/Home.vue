<template>
  <div class="home">
    <div class="feature-card">
        <router-link to="/movie/tt0409591"> <!-- tt3896198, tt0409591, tt1285016 -->

        <img src="./sonic.jpg" alt="Sonic Poster" class="featured-img" />
        <div class="detail">
          <h3>Sonic</h3>
          <p>A blue hedgehog with supersonic speed must rescue animals from being turned into robots by a mad scientist. Doctor Robotnik is an evil and mad scientist who only had one destiny, taking over the whole world and to do this he needs to collect all six chaos emeralds which are located on the South Island.</p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="What movie are you looking for?" class="text" v-model="search" />
      <input type="submit" value="Search" class="search">
    </form>

    <div class="movie-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">

            <img src="movie.Poster" alt="Movie Poster" /> <!-- src="movie.Poster" -->

            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail-search-item">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';

export default {
  setup () {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {        
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
            // console.log(data);
            // console.log(movies.value);
          });
        // console.log(search.value);
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<style scoped>
.home {
  
}
.feature-card {
  position: relative; 
}
.featured-img {
  display: block;
  width: 100%;
  height: 300px;
  object-fit: cover;

  position: relative;
  z-index: 0;
}

.detail {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  padding: 16px;
  z-index: 1;
}
h3 {
  color: #fff;
  margin-bottom: 16px;
}
p {
  color: #fff;
}

.search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 16px;
  align-items: center;
}
input {
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none;  
}
/**
$[type="text"] {
  width: 100%;
  color: #fff;
  background-color: #496583;
} **/
input.text {
  width: 100%;
  color: #fff;
  background-color: #496583;
  font-size: 20px;
  padding: 10px 16px;
  border-radius: 8px;
  margin-bottom: 15px;
  transition: 0.4s;
}
input::placeholder {
  color: #f3f3f3;
}
input::focus {
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}
input.text:focus {
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}
input.search {
  width: 300px;
  background: #428883;
  padding: 16px;
  border-radius: 8px;
  color: #fff;
  font-size: 20px;
  text-transform: uppercase;
  transition: 0.4s;
}
input.search:active {
  background-color: #388070;
}

.movie-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0px 8px;
}
.movie {
  max-width: 50%;
  flex: 1 1 50%;
  padding: 16px 8px;
}
.movie-link {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.product-image {
  position: relative;
  display: block;
}
img {
  display: block;
  width: 100%;
  height: 275px;
  object-fit: cover;
}
.type {
  position: absolute;
  padding: 8px 16px;
  background-color: #428883;
  color: #fff;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}

.detail-search-item {
  background-color: #496583;
  padding: 16px 8px;
  flex: 1 1 100%;
  border-radius: 0px 0px 8px 8px;
  /* border: 1px solid #fff; */
}
.year {
  color: #AAA;
  font-size: 14px;
}
h3 {
  color: #fff;
  font-weight: 600;
}
a { color: #fff;}
</style>


<!--
    // Original
    <router-link to="/movie/tt0409591">
    // Mine
    <router-link to="/movie/tt3896198">

        http://www.omdbapi.com/?i=tt3896198&apikey=a7c271f2

        http://www.omdbapi.com/?i=tt3896198&apikey=a7c271f2 /** tt0409591 **/

        // tt1285016
-->
