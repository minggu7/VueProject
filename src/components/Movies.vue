<template>
  <h1>영화 정보</h1>
  <div v-for="(movie) in movies" :key="movie.id" class="item">
    <figure>
      <img :src="movie.imgUrl" :alt="movie.title">
    </figure>
    <div>
      <h3 class="bg-black" :style="movie.textColor">{{ movie.title }}</h3>
      <p>{{ movie.year }}</p>
      <p>{{ movie.category }}</p>
      <button @click="$emit('likeUp', movie.id)">좋아요</button>
      <span>{{ movie.like }}</span>
      <p>
        <button @click="$emit('openModal', movie.id)">상세보기</button>
      </p>
    </div>
  </div>
</template>

<script>
  export default {
    name: "MoviesData",
    props: {
      movies: Array,
    }
  }

</script>

<style>

</style>