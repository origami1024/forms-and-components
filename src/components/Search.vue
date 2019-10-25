<template>
  <div class="search" :style="{'--bgc': bgc}">
    <input class="search__input" type="text" @keyup.enter="go" placeholder="Search" :style="inputStyle">
    <button class="search__btn" @click="go">
      <svg class="search__icon">
        <use fill="white" xlink:href="#mGlass"></use> 
      </svg>
    </button>
  </div>
</template>

<script>
export default {
  name: 'Search',
  props: {
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    inputStyle() {
      return `
      width: 100%;
      `
    }
  },
  methods: {
    go(){
      alert(1)
    }
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
  --bgc red
  margin 10px 0
  position relative
  display flex
  &__icon
    width 15px
    height 15px
  &__btn
    //position absolute
    border 0
    border-top-right-radius 3px
    border-bottom-right-radius 3px
    background-color var(--bgc)
    padding 0
    display flex
    justify-content center
    align-items center
    width 34px
    min-width 34px
    cursor pointer
.search__input
  background-color #E5E5E5
  border 0
  border-top-left-radius 3px
  border-bottom-left-radius 3px
  font-size 14px
  color #888888
  padding 6px 14px
  &::placeholder
    color #888888
  
</style>