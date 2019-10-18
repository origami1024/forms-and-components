<template>
  <div class="search" :style="wrapStyle">
    <input type="text">
    <button>+</button>
  </div>
</template>

<script>
export default {
  name: 'Search',
  props: {
    title: {type: String, default: 'BUTTON'},
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    wrapStyle() {
      return `
      background-color: ${this.bgc};
      `
    }
  },
  methods: {
  },
  mounted () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>

  
</style>