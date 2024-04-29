<template>
  <div class="detail-page">
    <img class="image" :src="getMoviePosterUrl(movie.Poster)" alt="Movie Poster" />
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Plot }}</p>
    <p><img class="rating" src="../assets/rating.svg"/> {{ movie.imdbRating }}</p>
  </div>
</template>

<script>
export default {
  async asyncData({ params }) {
    const movieId = params.id;
    try {
      const response = await fetch(`http://www.omdbapi.com/?i=${movieId}&apikey=7704cc7f`);
      const data = await response.json();
      return { movie: data };
    } catch (error) {
      console.error('Error fetching movie details:', error);
      return { movie: {} }; // Empty object in case of error
    }
  },
  methods: {
    getMoviePosterUrl(posterPath) {
      return posterPath; // Use the actual poster URL from the API response
    },
  },
};
</script>
<style>
.detail-page{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 4rem;
  margin-bottom: 1rem;
}
.image{
  border: 2px solid white;
}
.detail-page p{
  width: 50%;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
.rating{
  width: 24px;
  height: 20px;
  margin-right: 4px;
}
</style>
