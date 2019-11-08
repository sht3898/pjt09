<template>
  <div id="app">
    <div class="container">
      <!-- 1-3. 호출하시오. 
        필요한 경우 props를 데이터를 보내줍니다.
      -->
      <MovieList :movieList='movies' :genreList='genres'></MovieList>
    </div>
  </div>
</template>

<script>
const axios = require('axios');
// 1-1. 저장되어 있는 MovieList 컴포넌트를 불러오고,
import MovieList from './components/movies/MovieList.vue'

export default {
  name: 'app',
  // 1-2. 아래에 등록 후
  components: {
    MovieList
  },
  data() {
    return {
      // 활용할 데이터를 정의하시오.
      movies : [],
      genres : [],
    }
  },
  mounted() {
    // 0. mounted 되었을 때, 
    // 1) 제시된 URL로 요청을 통해 data의 movies 배열에 해당 하는 데이터를 넣으시오. 
    
    axios.get('https://gist.githubusercontent.com/banggeut01/ef5357321c299b40463be88fcf786e79/raw/d1d9932c72bfb189ad3dd1c058345a41038e826b/movie.json')
                  .then(response =>{
                    this.movies = response.data
                  })
    // 2) 제시된 URL로 요청을 통해 data의 genres 배열에 해당 하는 데이터를 넣으시오.
    axios.get('https://gist.githubusercontent.com/banggeut01/b7555e081d4c0e03f0651b4012d119b9/raw/64e58df2523436467575a1d7b6dc0c6ce82c2538/genre.json')
                  .then(response =>{
                    this.genres = [
                      {id: 0, name: '모두보기'},
                      ...response.data  // ...을 통해 배열을 object로 바꿈(spread 연산자)
                    ]
                  })
    
    console.log(this.movies)
    console.log(this.genres)
    // axios는 위에 호출되어 있으며, node 설치도 완료되어 있습니다.
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
