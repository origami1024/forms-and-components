<template>
  <select class="select" placeholder="Choose An Option">
    <option value="" disabled selected style="display:none;">Choose An Option</option>
    <option value="volvo">Volvo</option>
    <option value="saab">Saab</option>
    <option value="mercedes">Mercedes</option>
    <option value="audi">Audi</option>
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
  &:after
    background-color var(--bgc)
    position absolute
    content ''
    

  
</style>