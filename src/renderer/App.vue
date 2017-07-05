<template>
  <div style="webkit-app-region: drag">
    <carousel>
      <carouselSlide v-for="n in slides">
        <div class="text">Salut les gens</div>
        <img :src="'http://lorempicsum.com/futurama/800/450/' + n" width='100%'>
      </carouselSlide>
    </carousel>
  </div>
</template>

<script>
  import carousel from './components/carousel.vue'
  import carouselSlide from './components/carouselSlide.vue'

  export default {
    data () {
      return {
        slides: 6
      }
    },
    components: { carousel, carouselSlide }
  }

</script>

<style lang="sass">
body
  padding: 0
  margin: 0
img
  user-drag: none;
  -webkit-user-drag: none;
.text
  position: absolute
  color: white
  left: 0
  right: 0
  text-align: center
  top: 50%
  font-size: 2em
  font-family: arial
</style>
