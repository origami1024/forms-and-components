<template>
  <div class="search" :style="wrapStyle">
    <input class="search__input" type="text" placeholder="Search">
    <button>
      <svg class="search__icon" width=15 height=15>
        <use xlink:href="#mGlass"></use> 
      </svg>
    </button>
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
*
  margin 0
.search
  margin 10px 0
.search__input
  background-color #E5E5E5
  border 0
  border-top-left-radius 3px
  border-bottom-left-radius 3px
  font-size 14px
  color #888888
  padding 9px 14px
  &::placeholder
    color #888888
  
</style>