<template lang="pug">

  li.artist
    img(v-bind:src="artist.image[2]['#text']")
    h2: a(v-bind:href="artist.url" target="_blank") {{ artist.name }}

</template>

<script>
export default {
  name: 'artist',
  props: ['artist']
}

</script>

<style lang="stylus" scoped>

li.artist
  margin 5px
</style>

