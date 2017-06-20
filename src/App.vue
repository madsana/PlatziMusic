<template lang="pug">
  #app
    img(src='https://mnl1994.github.io/PlatziMusic/dist/logo.png')
    h1 Explorar

    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}

    spinner(v-show="loading")  
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
</template>

<script>
import artist from './components/Artist.vue'
import getArtists from './api'
import spinner from './components/Spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'Argentina', value: 'argentina'},
        { name: 'Colombia', value: 'colombia'},
        { name: 'España', value: 'spain'}
      ],
      selectedCountry: 'argentina', loading: true
    }
  },
  components: {
    artist,
    spinner
  },
  methods: {
    refreshArtists() {
        const self = this

        this.loading = true 
        this.artists = []
          getArtists(this.selectedCountry)
            .then(function (artists){
              self.loading = false
              self.artists = artists
      })  
    }
  },
  mounted() {
    this.refreshArtists()
  },
  watch: {
    selectedCountry() {
      this.refreshArtists()
    }
  }
}

</script>

<style lang="stylus">

body
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #fff
  margin-top 10px
  background #2d2d2d


h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  background #000

  padding 15px
  position relative
  cursor pointer
  transition 0.6s
  overflow hidden

a
  color #fff
  text-decoration none
  text-algin center

a:hover
  color #2c3e50

</style>
