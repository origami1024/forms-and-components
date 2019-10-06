<template>
  <div class="btnWrap" ref="btnwrapper" :style="wrapStyle">
  </div>
</template>

<script>
export default {
  name: 'Btn',
  props: {
    title: {type: String, default: 'BUTTON'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    wrapStyle() {
      return `
      background-color: ${this.bgc};
      padding-bottom: ${this.up ? !this.small ? this.sizes.normal[2] : this.sizes.small[2] : 0}px;
      `//padding-bottom: ${this.up ? !this.small ? this.sizes.normal[2] : this.sizes.small[2] : 0}px;
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
.btnWrap
  --wrapHoverbgcl pink
  position relative
  overflow hidden
  border-radius 3px
  align-self flex-end
  display flex
  flex-direction column
  transition-duration .3s
  &:hover
    background-color var(--wrapHoverbgcl) !important
.Btn
  --btnhoverbg coral
  align-self flex-end
  font-family 'Open Sans', sans-serif
  font-size 12px
  font-weight 600
  letter-spacing 1px
  box-sizing border-box
  border-radius: 3px;
  cursor: url("./../assets/img/theFingering.png"), auto;
  &:hover
    background-color var(--btnhoverbg) !important
    color white !important
    filter brightness(1.1)
  &:focus
    outline 0
.zoomer
  position absolute
  border-radius 100%
  width 1px
  height 1px
  background-color #fff
  pointer-events none
  opacity 0
  transition-duration 0.1s

.mDown
  opacity 0.5
  transform scale(50)
  
</style>