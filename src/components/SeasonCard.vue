<template>
  <div class="showCard">
        <b>{{season.name}}</b>
        <br/>
        <span class="episode-count">{{season.episode_count}} episodes</span>
  </div>
</template>

<script>
import moviedb from '../moviedb'
export default {
  name: 'SeasonCard',
  components: {
    
  },
  props: {
    season: Object,
  },
  data(){
    return {
    //   poster_url: '',
    }
  },
  async mounted() {
      moviedb.configuration().then(data=>{
          console.log(data)
        // this.poster_url = data.images.base_url
        // this.poster_url += data.images.poster_sizes[4]
      })
  },
  methods: {
    
  },
  computed: {

  }
}
</script>

<style scoped>
/* .showCard {
  max-width:600px;
  margin: auto;
  padding:10px;
  background:rgba(200,100,150,100);
  border-radius: 2rem;
}
ul {
    list-style-type: none;
}

.poster {
  max-height: 300px;
  float:left;
  padding:1rem;
}

.seasons-info{
  margin:auto;
  text-align: center;
  font-size: 1.3rem;
}

.episode-count{
  font-size:1rem;
}
.spacer{
  width:20px;
} */
</style>
