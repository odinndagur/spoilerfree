<template>
  <div>
  <form action="" @submit.prevent="searchTV" class="search-form">
    <input type="text"
    v-model="tvSearchString"
    placeholder="Search for a tv show"
    class="text-input">
    
    <input type="button"
    value="submit"
    class="button-input">
  </form>

  <showCard :tvShow="tvShow" />

  <!-- <ul>
    <li v-for="(key, value) in tvShow" :key="key + value">
      <b>{{key}} </b> {{value}} <br/>
    </li>
  </ul> -->

  </div>
</template>

<script>
import ShowCard from './ShowCard.vue'
import moviedb from '../moviedb'

export default {
  name: 'Home',
  components: {
    ShowCard
  },
  props: {
  },
  data(){
    return {
      tvSearchString: '',
      selectedShowId: -1,
      tvShow: {'lol':'ll'},
      searchResults: [],
    }
  },
  methods: {
    searchTV(){
      moviedb.searchTv({query:this.tvSearchString})
        .then(res => {
          this.searchResults = res.results;
          this.tvSearchString = '';
          moviedb.tvInfo({id:res.results[0].id})
            .then(show => this.tvShow = show)
        })
    }
  },
  mounted(){
    this.tvSearchString = 'Chicago PD';
    this.searchTV();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search-form{
  max-width:600px;
  margin: auto;
  padding:10px;
}

.text-input {
  min-width:15rem;
  height:2rem;
}

.button-input {
  height:2rem;
  
}
/* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} */
</style>
