<template>
  <button ref="arr" class="arrbtn" :class="{ arrleft: dir }" :style="{'--bgc': this.bgc, '--hcolor': this.hoverColor}"></button>
</template>

<script>
export default {
  name: 'ArrBtn',
  props: {
    dir: {type: Boolean, default: true}, //true = right, false = left
    bgc: {type: String, default: "blue"},
    hoverColor: {type: String, default: "blue"},
  },
  mounted () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.arrbtn
  --hcolor blue
  display block
  width 50px
  height 50px
  border-radius 100%
  background-color transparent
  cursor pointer
  border 3px solid var(--bgc)
  transition-duration .3s
  align-self flex-end
  &:active
    height 46px
  &:focus
    outline 0
  &:after
    display block
    width 16px
    height 16px
    border-top 4px solid var(--bgc)
    border-left 4px solid var(--bgc)
    content ''
    margin auto
    transform rotate(135deg)
    margin-right 10px
.arrleft
  &:after
    display block
    width 16px
    height 16px
    border-top 4px solid var(--bgc)
    border-left 4px solid var(--bgc)
    content ''
    margin auto
    transform rotate(-45deg)
    margin-left 10px

.arrbtn:hover
  background-color var(--hcolor)

.arrbtn:hover:after
  border-color white

.arrbtn:disabled
  border 3px solid #E5E5E5
  background-color #E5E5E5
  cursor auto
  pointer-events none

.arrbtn:disabled:after
  border-color white
</style>