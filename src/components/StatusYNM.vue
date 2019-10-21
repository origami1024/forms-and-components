<template>
<transition name="slide-fade" mode="out-in">
  <svg ref="ynm" class="ynm" :key="val" :style="wrapStyle" v-if="val!==undefined">
    <use xlink:href="#ynm" v-show="val!==undefined"></use>    
    <text x="50%" y="50%" v-show="val!==undefined" dominant-baseline="middle" text-anchor="middle" fill="white">{{val ? texty : textn}}</text>
  </svg>
</transition>
</template>

<script>
export default {
  name: 'StatusYNM', //STATUS: YES/NO/MAYBE
  props: {
    val: {type: Boolean, default: undefined}, //TRUE FALSE UNDEFINED, INVIS ON UNDEF
    texty: {type: String, default: 'THANKS!'},
    textn: {type: String, default: 'ERROR'},
    bgcy: {type: String, default: '#4EB7A8'},
    bgcn: {type: String, default: '#E75735'},
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
    shake() {
      this.$refs.ynm.classList.remove("shaking")
      setTimeout(() => {
        this.$refs.ynm.classList.add("shaking")
      }, 200);
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
.ynm
  width 75px
  min-width 75px
  height 28px
  font-size 11px
  font-family "Raleway", sans-serif
  box-sizing border-box
  animation-iteration-count 1
  animation-duration 0.5s
.shaking
  animation-name shake
  
.slide-fade-enter-active
  transition: all .3s ease;
.slide-fade-leave-active
  transition: all .4s cubic-bezier(1.0, 0.5, 0.8, 1.0);
.slide-fade-enter, .slide-fade-leave-to
  transform: rotateX(180deg);
  opacity: 0;



@keyframes shake {
  0% { transform: translate(1px, 1px) rotate(0deg); }
  10% { transform: translate(-1px, -2px) rotate(-1deg); }
  20% { transform: translate(-3px, 0px) rotate(1deg); }
  30% { transform: translate(3px, 2px) rotate(0deg); }
  40% { transform: translate(1px, -1px) rotate(1deg); }
  50% { transform: translate(-1px, 2px) rotate(-1deg); }
  60% { transform: translate(-3px, 1px) rotate(0deg); }
  70% { transform: translate(3px, 1px) rotate(-1deg); }
  80% { transform: translate(-1px, -1px) rotate(1deg); }
  90% { transform: translate(1px, 2px) rotate(0deg); }
  100% { transform: translate(1px, -2px) rotate(-1deg); }
}
</style>