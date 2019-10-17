<template>
  <form action="" class="fbform" v-on:submit.prevent="testSubmit">
    <div class="line">
      <input class="fbform__input" type="text" name="username" placeholder="Your Name" :style="inputDefStyle">
      <div class="fbform__tip err">ERROR</div>
    </div>
    <div class="line">
      <input class="fbform__input" type="text" name="email" placeholder="Your Email" :style="inputDefStyle">
      <StatusYNM />
      <!-- <div class="fbform__tip thx">THANKS!</div> -->
    </div>
    <div class="line"><textarea name="msg" placeholder="Your Message"></textarea></div>
    <div class="line">
      <Btn class="fbform__submitBtn" bgc="#4EB7A8" bgcl="#28A290" title="SUBMIT"/>
    </div>
  </form>
</template>

<script>
//TODO: validation while typing! with those error, thanks thingies
//WHAT KIND OF COMPONENT IS THAT ERROR/THANKS?
//like untickable tickbox vis/invis on isValid value?
//StatusYN component?
import Btn from './Btn.vue'
import StatusYNM from './StatusYNM.vue'
export default {
  name: 'FBForm',
  props: {
    title: {type: String, default: 'new group'}
  },
  data: function() {
    return {
      unValid: {type: Boolean, default: true},
      mailValid: {type: Boolean, default: true}
    }
  },
  components: {
    Btn,
    StatusYNM
  },
  computed: {
    inputDefStyle() {
      return `
      width: 100%;
      margin-right: 4px;
      `
    }
  },
  methods: {
    testSubmit(){
      //alert(1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.fbform
  width 290px
  box-sizing border-box

.line
  display flex
  justify-content space-between
  margin-bottom 11px
  width 100%
.exp
  width 100%
  background-color red
.fbform__input
	background-color #E5E5E5
	color #888888
	font-family Raleway, sans-serif
	border 0
	border-radius 3px
	padding 0 13px
	height 28px
	line-height 28px
	font-size 12px
	margin-right 4px
  letter-spacing 0.14px
  //flex 1 0 auto
  width 100%
textarea
  border-radius 3px
  background-color #e5e5e5
  font-family Raleway, sans-serif
  font-size 12px
  line-height 40px
  letter-spacing 0.14px
  color #888888
  border 0
  width 100%
  padding 0 13px
  height 89px
  resize none
.fbform__tip
  text-align center
  background-size 100% 100%
  width 75px
  min-width 75px
  height 28px
  font-size 11px
  font-family Raleway, sans-serif
  line-height 28px
  color white
  box-sizing border-box
  padding-left 4px
.err
  background url('./../assets/img/errbtn.svg')
  background-size 100% 100%
.thx
  background url('./../assets/img/thxbtn.svg')
  background-size 100% 100%
.fbform__submitBtn
  margin-left auto
</style>