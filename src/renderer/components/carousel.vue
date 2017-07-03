<template lang="pug">
  div.carousel
    slot
    button.carouselNav.carouselPrev(@click.prevent="prev") Precedent
    button.carouselNav.carouselNext(@click.prevent="next") Suivant
</template>

<script>
export default {
  data () {
    return {
      index: 0,
      slides: []
    }
  },
  mounted () {
    this.slides = this.$children
    this.slides.forEach((slide, i) => {
      slide.index = i
    })
  },
  computed: {
    slidesCount () { return this.slides.length }
  },
  methods: {
    next () {
      this.index++
      if (this.index >= this.slidesCount) {
        this.index = 0
      }
    },
    prev () {
      this.index--
      if (this.index < 0) {
        this.index = this.slidesCount - 1
      }
    }
  }
}
</script>

<style lang="sass">
  .carousel
    position: relative
    .carouselPrev, .carouselNext
      position: absolute
      top: 50%
      background: #000
      height: 20px
      width: 20px
    .carouselPrev
      left: 10px
    .carouselNext
      right: 10px
</style>
