<template>
  <div v-show="visible">
    <slot></slot>
    {{ index }}
    Visible ? {{ visible }}
  </div>
</template>

<script>
  export default {
    data () {
      return {
        index: 0
      }
    },
    computed: {
      visible () {
        return this.index === this.$parent.index
      }
    }
  }

</script>
