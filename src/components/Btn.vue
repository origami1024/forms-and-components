<template>
  <div class="btnWrap" ref="btnwrapper" :style="wrapStyle">
    <button class="Btn" ref="theBtn" :style="btnStyle" v-on="{ mousemove: mouseMove, mouseout: mouseOut, mousedown: mouseDown, mouseup: mouseUp}">{{title}}</button>
    <div class="zoomer" ref="zoomer"></div>
  </div>
</template>

<script>
//REDO THE CLICK ANIMATION!!!
export default {
  name: 'Btn',
  props: {
    title: {type: String, default: 'BUTTON'},
    bgc: {type: String, default: 'blue'},
    bgcl: {type: String, default: 'lightblue'},
    txtc: {type: String, default: 'white'},
    small: {type: Boolean, default: false},
    w: {type: Number, default: null}
  },
  data: function() {
    return {
      sizes: {normal: [119, 30, 3], small: [79, 24, 2]}, //width, height, padding-bottom of wrapper - make border smaller
      up: true
    }
  },
  computed: {//${this.bgc}
    btnStyle() {
      return `
      color: ${this.bgc}; 
      background-color: white;
      height: ${!this.small ? this.sizes.normal[1] : this.sizes.small[1]}px;
      width: ${this.w == null ? !this.small ? this.sizes.normal[0] : this.sizes.small[0] : this.w}px;
      border: 1px solid ${this.bgc};
      `
    },
    wrapStyle() {
      return `
      background-color: ${this.bgc};
      padding-bottom: ${this.up ? !this.small ? this.sizes.normal[2] : this.sizes.small[2] : 0}px;
      `//padding-bottom: ${this.up ? !this.small ? this.sizes.normal[2] : this.sizes.small[2] : 0}px;
    }
  },
  methods: {
    mouseMove(e){
      this.$refs.zoomer.style.left = e.offsetX + 'px'
      this.$refs.zoomer.style.top = e.offsetY + 'px'
    },
    mouseOut(e){
      this.$refs.zoomer.classList.remove('mDown')
      this.up = true
    },
    mouseDown(e){
      this.$refs.zoomer.classList.add('mDown')
      this.up = false
    },
    mouseUp(e){
      this.$refs.zoomer.classList.remove('mDown')
      this.up = true
    }
  },
  mounted () {
    this.$refs.theBtn.style.setProperty('--btnhoverbg', this.bgc)
    this.$refs.btnwrapper.style.setProperty('--wrapHoverbgcl', this.bgcl)
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
  &:focus
    outline 0
  &:active
    //
    //transform translateY(-3px)
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