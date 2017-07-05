<template lang="pug">
  .carousel
    slot
    button.carouselNav.carouselPrev(@click.prevent="prev")
    button.carouselNav.carouselNext(@click.prevent="next")
    .carouselPagination
      button(v-for="n in slidesCount" :class="{active: n-1 == index}" @click="goto(n-1)")
</template>

<script>
export default {
  data () {
    return {
      index: 0,
      slides: [],
      direction: null
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
    goto (index) {
      this.direction = index < this.index ? 'left' : 'right'
      this.index = index
    },
    next () {
      this.index++
      this.direction = 'right'
      if (this.index >= this.slidesCount) {
        this.index = 0
      }
    },
    prev () {
      this.index--
      this.direction = 'left'
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
    overflow: hidden
    .carouselPrev, .carouselNext
      outline: none
      cursor: pointer
      position: absolute
      top: 50%
      background: #000
      height: 20px
      width: 20px
    .carouselPrev
      left: 10px
    .carouselNext
      right: 10px
    .carouselPagination
      position: absolute
      bottom: 10%
      left: 0
      right: 0
      text-align: center
      button
        opacity: .5
        cursor: pointer
        height: 15px
        outline: none
        width: 15px
        background: #000
        margin-right: 1em
        border-radius: 100%
        border: none
        display: inline-block
      .active
        background: white
</style>
