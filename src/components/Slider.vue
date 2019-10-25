<template>
  <div style="display: flex; flex-direction: column; padding:18px 0;">
    <div :style="popStyle">{{val}}</div>
    <input ref="range" type="range" min="1" max="100" :value="val" style="" @input="onInput" :style="trunkStyle">
    <div class="ruler" :style="rulerStyle">
      <span class="ruler-tag">{{0}}</span>
      <span class="ruler-tag">{{Math.floor(maxval/4)}}</span>
      <span class="ruler-tag">{{Math.floor(maxval/4)*2}}</span>
      <span class="ruler-tag">{{Math.floor(maxval/4)*3}}</span>
      <span class="ruler-tag">{{maxval}}</span>
    </div>
  </div>
</template>

<script>
//v1.0
//idea - thumb as normal component. It gives better browser supp. Move it by transform - quicker with gpu, and u can do movement animations, like catching up to current pos and curved path of thumb movement
export default {
  name: 'Slider',
  props: {
    width: Number,
    val: Number,
    bgc: {type: String, default: '#E75735'},
    maxval: {type: Number, default: 100},
    showRuler: {type: Boolean, default: false},
    showPop: {type: Boolean, default: true},
    showGrad: {type: Boolean, default: true}
  },
  data: function() {
    return {
      popBgSVG: `url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' preserveAspectRatio='none' viewBox='0 0 35 28' width='35' height='28'><path d='M5,0h25a5,5,0,0,1,5,5v14a5,5,0,0,1-5,5h-6.082c-3.916,0-3.634,4.008-5.982,4.008-2.386,0-1.962-4.008-6.043-4.008H5a5,5,0,0,1-5-5V5A5,5,0,0,1,5,0Z' fill='${this.bgc.replace('#','%23')}'/></svg>"); `
    }
  },
  computed: {
    popStyle() {
      return "text-align:center; padding:5px; width:25px; height: 18px; font-size: 15px; line-height:15px; display: inline-block; background-image:" + this.popBgSVG + "background-size:100% 100%;position:relative; color: white;bottom: 12px; left:" + (parseInt(this.$props.val)*2 + 9) + "px; " + `visibility: ${this.showPop ? 'visible' : 'hidden'};`
    },
    rulerStyle() {
      return `padding-left: 5px; user-select: none; width: 220px; margin: 0 17px; display: flex; justify-content: space-between; font-size: 12px; padding-top: 8px; color: gray; visibility: ${this.showRuler ? 'visible' : 'hidden'};`
    },
    trunkStyle() {
      return `
      width: 220px;
      margin: 0 17px;
      cursor: pointer;
      ${this.showGrad ? `background-image: linear-gradient(90deg, ${this.bgc} ${this.val}%, transparent ${this.val}%);` : ''}
      
      `
    }
  },
  methods: {
    onInput: function (e) {
      this.$emit('update:val', parseInt(e.target.value))
    }
  },
  mounted () {
    this.$refs.range.style.setProperty('--thumbFill', this.bgc)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
thumb()
  -webkit-appearance none
  appearance none
  width 20px
  height 20px
  background var(--thumbFill)
  cursor pointer
  border-radius 100%
  border 0

input[type=range]
  --thumbFill pink
  --barFill #E5E5E5
  -webkit-appearance none
  appearance none
  width 200px
  height 5px
  background #E5E5E5
  outline none
  border-radius 2px
  margin 0 17px

input[type=range]::-webkit-slider-thumb
  thumb()

input[type=range]::-moz-range-thumb
  thumb()
  
</style>