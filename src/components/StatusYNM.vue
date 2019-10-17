<template>
  <svg class="ynm" :style="wrapStyle">
    <use xlink:href="#ynm" ></use>
    <text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" fill="white">{{val ? texty : textn}}</text>
  </svg>
</template>

<script>
//TODO: text doesnt change on invis(undefined), just style is invisible
//TRANSITION IN/OUT ANIMATION
export default {
  name: 'StatusYNM', //STATUS: YES/NO/MAYBE
  props: {
    val: {type: Boolean, default: undefined}, //TRUE FALSE UNDEFINED, INVIS ON UNDEF
    texty: {type: String, default: 'THANKS!'},
    textn: {type: String, default: 'ERROR'},
    bgcy: {type: String, default: 'blue'},
    bgcn: {type: String, default: 'red'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    wrapStyle() {
      return `
      fill: ${this.val? this.bgcy : this.bgcn};
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
.ynm
  //color white
  //text-align center
  //background-size 100% 100%
  width 75px
  min-width 75px
  height 28px
  font-size 11px
  font-family "Raleway", sans-serif
  //line-height 28px
  box-sizing border-box
  //padding-left 4px
  
</style>