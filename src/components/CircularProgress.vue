<template>
  <svg width="95" height=95 viewBox="0 0 36 36">
  <path v-show="value>0"
    d="M18 2.0845
      a 15.9155 15.9155 0 0 1 0 31.831
      a 15.9155 15.9155 0 0 1 0 -31.831"
    fill="none"
    :stroke="bgc"
    stroke-width="2"
    stroke-linecap=round
  >
    <animate attributeName="stroke-dasharray" dur="1s" from="0, 100" :to="`${value}, 100`" fill="freeze" />
  </path>
  <text fill="#9d9d9d" :x="value>9 ? 9 : 13" y="22" stroke="#9d9d9d" stroke-width=1>{{value}}</text>
</svg>
<!-- <div class="circularProgress" :style="wrapStyle">{{value}}</div> -->
<!-- :stroke-dasharray="`${value}, 100`" -->
</template>

<script>
export default {
  name: 'CircularProgress',
  props: {
    value: {type: Number, default: 0},
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
    }
  },
  computed: {
  },
  methods: {
  },
  mounted () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.circularProgress
  width 85px
  height 85px
  text-align center
  line-height 85px
  border 5px solid transparent
  position relative
  border-radius 100%
  font-size 40px
  color #9d9d9d

</style>