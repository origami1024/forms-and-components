<template>
  <div class="toggle" ref="toggle" :style="toggleStyle" @click="change" @mouseenter="mMove" @mouseleave="mOut" @mousedown="mDown" @mouseup="mUp" @>
    <span class="toggle__label" :class="{'toggle__label--on': value}" :style="labelStyle">{{value ? 'ON' : 'OFF'}}</span>
    <span class="toggle__thumb" :class="{'toggle__thumb--on': value}" :style="thumbStyle"></span>
  </div>
</template>

<script>
export default {
  name: 'Toggle',
  props: {
    value: {type: Boolean, default: false},
    bgc: {type: String, default: 'blue'},
    col: {type: String, default: 'white'},
  },
  data: function() {
    return {
      thumbX: 0,
      thumbScale: 1,
      labelScaleY: 1,
      labelX: 0
    }
  },
  computed: {
    toggleStyle() {
      return `
        background-color: ${this.value ? this.bgc : 'gray'};
        color: ${this.col};
      `
    },
    thumbStyle() {
      return `
        background-color: ${this.col};
        transform: translateX(${this.thumbX}px) scale(${this.thumbScale});
      `
    },
    labelStyle() {
      return `
        transform: translateX(${this.labelX}px) scaleY(${this.labelScaleY});
      `
    }
  },
  methods: {
    change(){
      this.$emit('update:value', !this.value)
    },
    mMove(e){
      this.labelScaleY = 1.2
    },
    mOut(e){
      this.labelScaleY = 1
      this.thumbScale = 1
    },
    mDown(e){
      this.thumbScale = 1.2
    },
    mUp(e){
      this.thumbScale = 1
    }
  },
  watch: {
    value: function(newV, oldV){
      this.thumbX = newV ? 37 : 0
      this.labelX = newV ? -14 : 0
    }
  },
  mounted () {
    this.thumbX = this.value ? 37 : 0
    this.labelX = this.value ? -14 : 0
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.toggle
  --height 25px
  --thumb-rad calc(var(--height) - 8px)
  width 60px
  height var(--height)
  line-height var(--height)
  border-radius 12px
  font-family Raleway, sans-serif
  letter-spacing 0.6px
  font-size 12px
  position relative
  cursor pointer
  transition-duration .5s
  &:active
    //
  &:active>.toggle__thumb
    //transform translateX(0) scale(1.2)
  &:hover
    filter brightness(1.2)
    &>.toggle__label
      //transform translateX(-15px) scaleY(1.2)
      animation-name foo
    &>.toggle__thumb
      //animation-name foo
  &__label
    display block
    position absolute
    user-select none
    left calc(50% - 5px)
    top calc(50% - 12px)
    transition-duration .6s
    animation-duration .7s
    animation-iteration-count infinite
    animation-direction alternate
    &--on
      //transform translateX(15px) scaleY(1)
      
  &__thumb
    display block
    width var(--thumb-rad)
    height var(--thumb-rad)
    border-radius 100%
    position absolute
    top calc(50% - (var(--thumb-rad) / 2))
    left 3px
    transition-duration .15s
    &--on
      //transform translateX(37px)
@keyframes foo {
  to {
    opacity: 0.6;
  }
}
</style>