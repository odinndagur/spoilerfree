<template>
  <div class="showCard">
    <div class="main-info">
      <img :src="poster_url + tvShow.poster_path" alt="" class="poster">
      <h1>{{tvShow.original_name}}</h1>
      <p>{{tvShow.overview}}</p>
        <!-- <div v-for="season in tvShow.seasons" :key="season"> -->
          <!-- <b>{{season.name}}:</b> <span class="spacer">       </span>{{season.episode_count}} episodes -->
        <!-- </div> -->
    </div>

    <div class="seasons-info">
            <h3>{{tvShow.number_of_seasons}} seasons</h3>
        <seasonCard v-for="season in tvShow.seasons" :season="season" :key="season">
            <!-- <b>{{season.name}}</b>
            <br/>
            <span class="episode-count">{{season.episode_count}} episodes</span> -->
        </seasonCard>
    </div>
  </div>
</template>

<script>
import moviedb from '../moviedb'
import SeasonCard from './SeasonCard.vue'

export default {
  name: 'ShowCard',
  components: {
    SeasonCard,
  },
  props: {
    tvShow: Object,
  },
  data(){
    return {
      poster_url: '',
    }
  },
  async mounted() {
      moviedb.configuration().then(data=>{
        this.poster_url = data.images.base_url
        this.poster_url += data.images.poster_sizes[4]
      })
  },
  methods: {
    
  },
  computed: {

  }
}
</script>

<style scoped>
.showCard {
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
}
</style>
