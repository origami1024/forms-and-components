<template>
  <div class="tickbox" ref="tickbox" :style="tickBoxStyle" @click="change">
    <transition name="bounce">
      <span class="ticked" v-show="value"></span>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'Tickbox',
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
    tickBoxStyle() {
      return `
        background-color: ${this.value ? this.bgc : 'gray'};
        color: ${this.value ? this.col : 'darkgray'};
      `
    }
  },
  methods: {
    change(){
      this.$emit('update:value', !this.value)
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
//ANIM IDEA - SCALE IT TO SMALL AND HIDE
.tickbox
  border-radius 100%
  max-width 25px
  width 25px
  min-height 25px
  height 25px
  position relative
  cursor pointer
  transition-duration .3s
  &:hover
    filter brightness(1.2)
  &:hover>.ticked
    //animation-name foo
  &:active>.ticked
    //animation-name none
    
.ticked
  --height 12px
  //--tcikedCenter calc(var(--height) - )
  display block
  margin 0 auto
  height 6px
  width 10px
  border-bottom 2px solid white
  border-left 2px solid white
  background-color transparent
  transition-duration .3s
  transform scale(1) rotateZ(-45deg)
  position absolute
  top calc(50% - (var(--height) / 2))
  left calc(50% - (var(--height) / 2))
  animation-iteration-count infinite
  animation-duration 5s
  animation-timing-function linear

.bounce-enter-active
  animation bounce-in .5s

.bounce-leave-active
  animation bounce-in .5s reverse

@keyframes bounce-in{
    0% {
    transform scale(0) rotateZ(-45deg)
    }

50%{
  transform scale(1.5) rotateZ(-45deg)
}
100%{
  transform scale(1) rotateZ(-45deg)
}
}
</style>