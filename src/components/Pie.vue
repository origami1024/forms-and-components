<template>
  <div class="pie" >
    <div class="pie__seg" v-for="(seg, i) in segz" :key="i" :style="{transform: `translate(0, -50%) rotate(90deg) rotate(${degsBefore(i)}deg)` }">
      <span class="pie__segfill" :style="{
        background: `radial-gradient(circle at center top, transparent 31px, ${seg[1]?seg[1]:'blue'} 32px)`,
        transform: `translate(0, 100%) rotate(${seg[0] + 1}deg)`
        }">
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Pie',
  props: {
    segs: {type: Function, default: ()=>{return [[45,'DimGray'],[90],[110,'green']]}},
    bgc: {type: String, default: 'gray'},
  },
  data: function() {
    return {
      segz: [[45,'DimGray'],[90,'red'],[173,'green']]
    }
  },
  computed: {
    segStyle() {
      return `
      background-color: ${this.bgc};
      transform: translate(0, -50%) rotate(90deg) rotate(0deg);
      `
    }
  },
  methods: {
    degsBefore(i){
      let res = 0
      for (let index = 0; index < i; index++) {
        res += this.segz[index][0]
      }
      return res
    },
    breakSegs() {
      let newVal = this.segs()
      let res = []
      let breaker360 = 0
      for (let index = 0; index < newVal.length; index++) {
        if (breaker360 + newVal[index][0] > 360) {
          newVal[index][0] = 360 - breaker360
        }
        breaker360 += newVal[index][0]
        if (newVal[index][0] < 180) {
          res.push(newVal[index])
        } else {
          res.push([newVal[index][0]/2,newVal[index][1]])
          res.push([newVal[index][0]/2,newVal[index][1]])
        }
        if (breaker360>=360) break
      }
      this.segz = res
    }
  },
  watch: { 
    segs: function() { // watch it
      //console.log('Prop changed: ', newVal, ' | was: ', oldVal)
      this.breakSegs()
    }
  },
  mounted () {
    this.breakSegs()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.pie
  height 95px
  position relative
  width 95px
  border-radius 100%
  overflow hidden
  background radial-gradient(transparent 31px, #E5E5E5 31px)
  pointer-events none
.pie__seg
  box-sizing border-box
  height 100%
  width 100%
  position absolute
  top 0
  left 0
  transform-origin 50% 100%
  overflow hidden
.pie__segfill
  content ''
  height 100%
  width 100%
  top 0
  left 0
  position absolute
  transform-origin 50% 0
  
    
</style>