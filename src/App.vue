<template lang="pug">
  #app
    img(src="https://aspivina.github.io/Basic-VueJS/src/assets/logo.png")
    h1 Platzi Music
    select(v-model="selected_country")
      option(v-for="country in countries" :value="country.value") {{country.name}}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" :key="artist.mbid")

</template>

<script>
import getArtists from './api'
import artist from './components/artist.vue'
import spinner from './components/spinner.vue'

export default {
  name: 'app',

  data () {
    return {
      artists: [],
      countries:[
        {name:'Argentina', value:'argentina'},
        {name:'Colombia', value:'colombia'},
        {name:'España', value:'spain'},
      ],
      selected_country: 'argentina',
      loading: true
    }
  },
  components:{
    artist : artist,
    spinner : spinner
  },
  methods: {
    refresh_artists(){
      const self = this
      this.loading = true
      this.artist=[]
      getArtists(this.selected_country)
        .then(function(artists){
          self.loading = false
          self.artists = artists
        })      
    }
  },
  mounted(){
    this.refresh_artists() //permite inicializar con los datos por defecto
  },
  watch: {
    selected_country(){
      this.refresh_artists() //cambiar los artistas  según el nuevo pais seleccionado
    }
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

h1, h2, a {
  font-weight: normal;
  color: #2c3e50;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}



</style>
