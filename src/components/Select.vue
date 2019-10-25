<template>
  <select class="select" placeholder="Choose An Option" :style="selectStyle">
    <option value="" disabled selected style="display:none;">Choose An Option</option>
    <option v-for="option in input()" :value="option.val" :key="option.val">{{option.inner}}</option>
  </select>
</template>

<script>
//receive list of items
//syncronize wot is picked with parent
//custom style for the button
//custom style for visible text
export default {
  name: 'Select',
  props: {
    input: {type: Function, default: ()=>{return[
      {val: 'volvo', inner: 'Volvo'},
      {val: 'saab', inner:  'Saab 1'},
      {val: 'mercedes', inner:  'Mercedes'},
      {val: 'audi', inner: 'Audi'}
    ]}},
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    selectStyle() {
      return `
      --bgc: ${this.bgc};
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

.select
  --bgc pink
  background-color #E5E5E5
  border 0
  border-top-left-radius 3px
  border-bottom-left-radius 3px
  font-size 14px
  color #888888
  padding 6px 14px
  appearance none
  position relative
  background-image url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='18' height='13'><polyline stroke='white' fill='none' stroke-width='2' vector-effect='non-scaling-stroke' points='0,0 8,8 17,0' stroke-linejoin='round'></polyline></svg>"), linear-gradient(to left, var(--bgc), var(--bgc) 34px, transparent 34px)
  background-repeat no-repeat
  background-position calc(100% - 7px) calc(50% + 3px), 0 0
  cursor pointer
  &:after
    background-color red
    position absolute
    content 'aaaaaaaaass'
    width 11px
    height 11px
    border 2px solid #fff
    top 50%
    right 10px

  
</style>