<template>
  <div class="message" :style="wrapStyle">
    <div class="message__top" :style="topStyle">
      <h2 class="message__header">{{mdata().uname}}</h2>
    </div>
    <div class="message__midControls">
      <div class="btn">1</div>
      <Userpicture class="message__img" :img="mdata().img" :bgposx="mdata().bgposx" :bgposy="mdata().bgposy"/>
      <div class="btn">2</div>
    </div>
    <div class="message__content">...</div>
    <div class="message__responce">...</div>
    <Btn bgc="#4EB7A8" bgcl="#28A290" title="REPLY"/>
    
  </div>
</template>

<script>
import Btn from './Btn.vue'
import Userpicture from './Userpicture.vue'
export default {
  name: 'Message',
  props: {
    bgc: {type: String, default: 'blue'},
    bgc2: {type: String, default: 'aquamarine'},
    mdata: {type: Function, default: ()=>{return{
        uname: 'Defaulto',
        img: require('./../assets/img/sarah.png'),
        incMsg: 'Hey! So are we cool to meet at the art gallery? Say 8pm',
        bgposx: -85,
        bgposy: 135
      }}}
  },
  data: function() {
    return {
    }
  },
  components: {
    Btn,
    Userpicture
  },
  computed: {
    wrapStyle() {
      return ``
    },
    topStyle() {
      return `
      background-color: ${this.bgc};
      border-bottom: 35px solid ${this.bgc2};
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
*
  margin 0
.message
  min-width 290px
  color white
  background-color #F2F2F2
  &__top
    padding-top 22px
    padding-bottom 26px
    font-family "Open sans", sans-serif
    font-size 18px
    //
  &__midControls
    //
  
</style>