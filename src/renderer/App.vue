<template>
  <div>
    <carousel>
      <carouselSlide>
        Salut les gens
        <img src="http://lorempicsum.com/futurama/630/300/1">
      </carouselSlide>
      <carouselSlide>
        Au revoir les gens
        <img src="http://lorempicsum.com/futurama/630/300/2">
      </carouselSlide>
    </carousel>
  </div>
</template>

<script>
  import carousel from './components/carousel.vue'
  import carouselSlide from './components/carouselSlide.vue'

  export default {
    components: { carousel, carouselSlide }
  }

</script>

<style>
  /* CSS */
</style>
