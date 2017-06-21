<template lang="pug">
#app
  h1.title PlatziMusic
  select(v-model="selectedCountry")
    option(v-for="country in countries" :value="country.value") {{ country.name }}
  spinner(v-show="loading")
  ul
    artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid") {{ artist.name }}

</template>
<script>
import Artist from './components/Artist.vue'
import getArtists from './api'
import Spinner from './components/spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Brazil', value: 'brazil'},
        {name: 'Colombia', value: 'colombia'},
        {name: 'España', value: 'spain'},
        {name: 'Mexico', value: 'mexico'},
        {name: 'Argentina', value: 'argentina'},
        {name: 'Ecuador', value: 'ecuador'},
      ],
      selectedCountry: 'colombia',
      loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      const self = this
      this.artists = []
      this.loading = true
      getArtists(this.selectedCountry)
        .then(function (artists) {
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
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
body
  margin 0
#app
  margin 0
select
  margin-top 50px
  border 1px solid #339966
  color #339966
  font-size 16px


h1.title
  margin 0
  font-size 60px
  margin 0 auto
  background #339966
  color #fff

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983

</style>
