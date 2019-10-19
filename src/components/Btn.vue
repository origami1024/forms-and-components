<template>
  <div class="btnWrap" :style="wrapStyle">
    <button :disabled="disabled" class="Btn" :style="btnStyle" v-on="{ mousemove: mouseMove, mouseout: mouseOut, mousedown: mouseDown, mouseup: mouseUp}">{{title}}</button>
    <span class="ripple" ref="ripple" v-on:animationend="rippleEnd" :style="rippleStyle"></span>
  </div>
</template>

<script>
export default {
  name: 'Btn',
  props: {
    title: {type: String, default: 'BUTTON'},
    bgc: {type: String, default: 'blue'},
    bgcl: {type: String, default: 'lightblue'},
    txtc: {type: String, default: 'white'},
    small: {type: Boolean, default: false},
    takefull: {type: Boolean, default: false},
    w: {type: Number, default: null},
    disabled: {type: Boolean, default: false},
  },
  data: function() {
    return {
      sizes: {normal: [119, 30, 3], small: [79, 24, 2]}, //width, height, padding-bottom of wrapper - make border smaller
      up: true
    }
  },
  computed: {
    btnStyle() {
      return `
        --btnhoverbg: ${this.bgc};
        color: ${this.bgc}; 
        background-color: white;
        height: ${!this.small ? this.sizes.normal[1] : this.sizes.small[1]}px;
        ${this.takefull ? 'width: auto;' : `width: ${this.w == null ? !this.small ? this.sizes.normal[0] : this.sizes.small[0] : this.w}px;`}
        border: 1px solid ${this.bgc};
      `//${this.takefull ? 'width: auto;': ''}
    },
    wrapStyle() {
      return `
        --wrapHoverbgcl: ${this.bgcl};
        background-color: ${this.bgc};
        ${this.takefull ? 'width: auto;' : `width: ${this.w == null ? !this.small ? this.sizes.normal[0] : this.sizes.small[0] : this.w}px;`}
        padding-bottom: ${this.up ? !this.small ? this.sizes.normal[2] : this.sizes.small[2] : 0}px;
        margin-top: ${!this.up ? !this.small ? this.sizes.normal[2] : this.sizes.small[2] : 0}px;
        ${this.disabled ? 'filter: grayscale(100%); pointer-events: none;' : null}
        
      `
    },
    rippleStyle() {
      return `
        background-color: white;
        opacity: 0.7;
        display: none;
        border-radius: 100%;
        position: absolute;
        transition-duration: 0;
        width: 200px;
        height: 200px;
        border-radius: 100%;
        pointer-events: none;
        left: 0px;
        top: 0px;
        z-index: 1;
      `
    }
  },
  methods: {
    mouseMove(){
    },
    mouseOut(){
      this.up = true
    },
    mouseDown(e){
      this.animateRipple(e.offsetX,e.offsetY)
      this.up = false
      
    },
    mouseUp(){
      this.up = true
    },
    animateRipple(x, y) {
			//let el  = this.$refs.tiBtn;
      //let pos = this.$refs.getBoundingClientRect();
      this.$refs.ripple.style.left = (x - 100) + 'px'
      this.$refs.ripple.style.top = (y - 100) + 'px'
      this.$refs.ripple.style.display = 'block'
      this.$refs.ripple.classList.remove('rippleAnimClass')
      void this.$refs.ripple.offsetWidth;
      this.$refs.ripple.classList.add('rippleAnimClass')
      
    },
    rippleEnd: function() {
      this.$refs.ripple.style.display = 'none'
		}
  },
  mounted () {
    //this.$refs.theBtn.style.setProperty('--btnhoverbg', this.bgc)
    //this.$refs.btnwrapper.style.setProperty('--wrapHoverbgcl', this.bgcl)
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
.disabled
  pointer-events none
.Btn
  --btnhoverbg coral
  position relative
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
  width 50px
  height 50px
  background-color #fff
  pointer-events none
  opacity 0
  transition-duration 0.1s
  transform scale(0.1)


.rippleAnimClass
  animation-name ripple
  animation-duration 1s
@keyframes ripple {
	0%   { transform: scale(0); }
	80%  { transform: scale(0.8); }
	100% { transform: scale(1); opacity: 0; }
}
</style>