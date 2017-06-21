<template lang="pug">
  li.artist
    h2: a(:href="artist.url" target="_blank") {{ artist.name }}
    img(:src="artist.image[3]['#text']")
    div.container-desc
      p.description {{ artist.listeners}}
      p.listenner Reproducciones
</template>

<script>
export default {
  name: 'artist',
  props: ['artist']
}
</script>

<style lang="stylus" scoped>
  li.artist
    margin 10px 20px

  img
    border-radius 5px

  .container-desc
    background #339966
    border-radius 5px
    padding 8px
    display flex
    justify-content space-between
    align-items center
    color #fff

  .description
    color #fff
    border-radius 5px
    border 1px solid #fff
    padding 3px 6px
    margin 0
  .listenner
    margin 0

</style>
