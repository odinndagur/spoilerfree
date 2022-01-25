<template>
  <div>
<h1>lol</h1>
  <form action="" @submit.prevent="searchTV">
    <input type="text"
    v-model="tvSearchString"
    placeholder="Search for a tv show">
    <input type="button" value="submit">
  </form>

  <showCard :tvShow="tvShow" />

  <ul>
    <li v-for="(key, value) in tvShow" :key="key + value">
      <b>{{key}} </b> {{value}} <br/>
    </li>
  </ul>

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
