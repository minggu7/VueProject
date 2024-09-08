<template>
  <Navbar />
  <Event :text="text[eventTextIndex]"/>
  <SearchBar :movies="movies_temp" @searchMovie="searchMovie($event)"
            />
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>
  <MoviesData :movies="movies_temp"
              @openModal="openModal"
              @likeUp="likeUp"
              />
  <MovieModal :movies="movies"
              :isModal="isModal"
              :selectedMovie="selectedMovie"
              @closeModal="isModal=false"
              />
</template>

<script>
import movies from './assets/movies'; // 영화 데이터
import Navbar from './components/Navbar.vue'; // 네비게이션 바
import MovieModal from './components/MovieModal.vue'; // 모달 창
import MoviesData from './components/Movies.vue';//영화 정보
import Event from './components/Event.vue';//이벤트 박스
import SearchBar from './components/SearchBar.vue';//검색 기능

export default {
  name: 'App',
  data() {
    return {
      isModal: false,
      like: 0,
      movies: movies, //영화 원본
      movies_temp : [...movies],//영화 사본
      selectedMovie: 0, // 선택된 영화의 인덱스
      text: [
        '오늘의 무료 영화',
        '20대 인기 영화',
        '실시간 1위 애니메이션'
      ],
      eventTextIndex: 0,
      interval: null,
    };
  },
  methods: {
    likeUp(id) {
    const movie = this.movies_temp.find(movie => movie.id === id);
    if (movie) {
      movie.like += 1;
    }
  },
    openModal(i) {
      this.selectedMovie = i;
      this.isModal = true;
    },
    searchMovie(title){
      //영화 제목 받아오기
      //받아온 입력값과 영화 배열 제목값을 비교.
      this.movies_temp = this.movies.filter(movie => {
        return movie.title.includes(title);
      })
    },
    showAllMovie(){
      this.movies_temp = [...this.movies]
    }
  },
  components: {
    Navbar: Navbar,
    MovieModal: MovieModal,
    MoviesData: MoviesData,
    Event: Event,
    SearchBar: SearchBar,
  },
  mounted() {
    console.log('mounted');
    this.interval = setInterval(() => {
      if(this.eventTextIndex == this.text.length - 1){
        this.eventTextIndex = 0;
      }else{
        this.eventTextIndex +=1;
      }
  }, 3000)
  },
  unmounted() {
    clearInterval(this.interval); //인터발 해제
  }
};
</script>

<style>
    * {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: #121212;
  color: #e0e0e0;
  max-width: 768px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

h1, h2, h3 {
  margin-bottom: 1rem;
  color: #ffffff;
}

p {
  margin-bottom: 0.5rem;
  color: #b3b3b3;
}

button {
  background-color: #333;
  color: #fff;
  border: 1px solid #444;
  padding: 10px 20px;
  cursor: pointer;
  margin-right: 10px;
  margin-top: 1rem;
}

button:hover {
  background-color: #444;
}

.item {
  background-color: #1f1f1f;
  border: 1px solid #333;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
  border-radius: 8px;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
  border-radius: 8px;
}

.item .info {
  width: 100%;
  color: #ffffff;
}

.modal {
  background: rgba(0, 0, 0, 0.9);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal .inner {
  background: #262626;
  color: #e0e0e0;
  width: 80%;
  padding: 20px;
  border-radius: 10px;
}

.navbar {
  background: #000;
  padding: 20px;
}

.navbar a {
  color: #ffffff;
  text-decoration: none;
  padding: 1em;
}

.search-box {
  display: flex;
  background-color: #1f1f1f;
  border: 1px solid #333;
  padding: 10px;
  border-radius: 8px;
}

.search-box input {
  background-color: #333;
  color: #fff;
  border: none;
  flex-grow: 1;
  padding: 10px;
  border-radius: 8px;
  margin-right: 10px;
}

.search-box button {
  background-color: #444;
  color: #fff;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 8px;
}

.search-box button:hover {
  background-color: #555;
}
</style>
