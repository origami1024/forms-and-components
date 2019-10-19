<template>
  <transition name="slide-fade" mode="out-in">
    <form action="" v-if="!sent" class="fbform" v-on:submit.prevent="submit">
      <div class="line">
        <input v-model="uname" class="fbform__input" type="text" name="username" placeholder="Your Name" :style="inputDefStyle">
        <StatusYNM :val="unValid"/>
      </div>
      <div class="line">
        <input v-model="mail" class="fbform__input" type="text" name="email" placeholder="Your Email" :style="inputDefStyle">
        <StatusYNM :val="mailValid" />
      </div>
      <div class="line"><textarea name="msg" placeholder="Your Message"></textarea></div>
      <div class="line">
        <Btn class="fbform__submitBtn" bgc="#4EB7A8" bgcl="#28A290" title="SUBMIT" :disabled="!(unValid && mailValid)"/>
      </div>
    </form>
    <div v-if="sent" class="fbform__sent">
      <p>data has been sent</p>
    </div>
  </transition>
</template>

<script>
//TODO: on submit - transition the form out, play loading animation, and then leave like thonx!
import Btn from './Btn.vue'
import StatusYNM from './StatusYNM.vue'
export default {
  name: 'FBForm',
  props: {
    // title: {type: String, default: 'new group'}
  },
  data: function() {
    return {
      uname: '',
      mail: '',
      unValid: undefined, //boolean + undefined
      mailValid: undefined,
      sent: false
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
  watch: {
    uname: function (val) {
      let unameRegExp = /^[A-Za-z][A-Za-z0-9]{5,25}$/
      this.unValid = unameRegExp.test(val)
    },
    mail: function (val) {
      let mailRegExp = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      this.mailValid = mailRegExp.test(val)
    }
  },
  methods: {
    submit(){
      this.sent = true
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

.fbform__sent
  color black

.slide-fade-enter-active
  transition all .3s ease
.slide-fade-leave-active
  transition all .4s cubic-bezier(1.0, 0.5, 0.8, 1.0)
.slide-fade-enter, .slide-fade-leave-to
  transform rotateX(180deg)
  opacity 0
</style>