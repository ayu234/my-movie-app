<template>
  <div class="custom-container">
   <h1>Movie Posters</h1>
  <div class="custom-row">
    <div class="custom-col" v-for="movie in movies" :key="movie.imdbID">
      <div class="custom-card">
      <img :src="getMoviePosterUrl(movie.Poster)" alt="Movie Poster" @click="goToMovieDetails(movie.imdbID)" />
    </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  async asyncData() {
    try {
      const response = await fetch('http://www.omdbapi.com/?s=Batman&apikey=7704cc7f');
      const data = await response.json();
      return { movies: data.Search };
    } catch (error) {
      console.error('Error fetching movie data:', error);
      return { movies: [] }; // Empty array in case of error
    }
  },
  methods: {
    getMoviePosterUrl(posterPath) {
      return posterPath; // Use the actual poster URL from the API response
    },
    goToMovieDetails(movieId) {
      this.$router.push(`/movie/${movieId}`);
    },
  },
};
</script>
<style>
.custom-container {
   max-width: 1320px;
    padding-right: 15px;
    padding-left: 15px;
    margin-right: auto;
    margin-left: auto;
}

/* Custom row */
.custom-row {
  display: flex;
    flex-wrap: wrap;
    margin-right: -15px;
    margin-left: -15px;
    align-items: center;
    justify-content: center;
}



/* Responsive adjustments using media queries */
@media (min-width: 1024px) {
  .custom-row {
    justify-content: start;
}

}

@media (min-width: 768px) {
  /* ... existing styles */
}

/* Custom column */
.custom-col {
  position: relative;
    width: 100%;
    padding-right: 15px;
    padding-left: 15px;
    flex: 0 0 22%;
    max-width: 100%;
    margin-bottom: 28px;
    cursor: pointer;
}
.custom-card{
  border: 2px solid white;
}
.custom-card img{
  width: 19rem;
  height: 28rem;
}
h1{
  color: white;
  font-weight: 500;
  text-align: center;
  margin-top: 40px;
  margin-bottom: 40px;
}
/* Base styles for custom card content */

</style>
