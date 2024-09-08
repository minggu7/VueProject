<template>
  <div class="search-box">
    <input type="search"
    @change="
    $emit('searchMovie', $event.target.value)
    inputText = $event.target.value;
    $event.target.value = ''"
    placeholder="검색어를 입력 해주세요">
    <button>검색</button>
  </div>
</template>

<script>
  export default{
    name: 'SearchBarComponent',
    data(){
      return{
        inputText: '',
      }
    },
    props: {
      movies: Array,
    },
    watch: {
      inputText(moviename){
        // 입력한 영화제목이 데이터에 있는지 확인
        const findMovies = this.movies.filter(movie => {
          return movie.title.includes(moviename);//includes로 인해 한 글자만 일치해도 출력 됨
        })

        if(findMovies != ""){
          alert("찾는 영화가 있습니다");
        }else{
          alert("찾는 영화는 없습니다")
        }
      }
    }
  }
</script>

<style>
  .search-box{
    display: flex;
  }

  .search-box{
    padding: 5px, 10px;
  }

  .search-box button{
    margin: 0;
  }
</style>