<template>
  <div class="stages" :style="stagesStyle">
    <span class="stages__circle" v-for="item in partsNum" :key="item" :style="{left: `calc((${item} - 1) / (${partsNum} - 1) * (100% - 30px))`, backgroundColor: item<=current ? bgc : '#E5E5E5', color: item<=current ? '#fff' : '#888'}">{{item}}</span>
  </div>
</template>

<script>
//props - number of points!!! so its v-for or smth!
//the bar itself is gradient bg
export default {
  name: 'Stages',
  props: {
    partsNum: {type: Number, default: 5}, //total number of circles
    current: {type: Number, default: 3}, //current fill till what circle
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    stagesStyle() {
      return `
        background-image: linear-gradient(90deg, ${this.bgc} 0%, ${this.bgc} ${((this.current - 1) * 100) / (this.partsNum - 1)}%, transparent ${((this.current - 1) * 100) / (this.partsNum - 1)}%);
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
.stages
  width 100%
  height 5px
  display flex
  position relative
  background-color #E5E5E5
  box-sizing border-box
  margin 10px 0
.stages__circle
  min-width 30px
  max-width 30px
  min-height 30px
  max-width 30px
  line-height 30px
  top -13px
  background-color #E5E5E5
  position absolute
  border-radius 100%
  color #888

</style>