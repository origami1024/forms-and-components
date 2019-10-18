<template>
  <div class="message" ref="message" :style="wrapStyle">
    <form action="#" v-on:submit.prevent="testSubmit">
      <div class="message__top" :style="topStyle">
        <h2 class="message__header">{{mdata().uname}}</h2>
      </div>
      <div class="message__midControls">
        <a href="#" class="message__btns">
          <svg width="20" height="21">
            <use xlink:href="#chat" ></use>
          </svg>
        </a>
        <Userpicture class="message__img" :img="mdata().img" :bgposx="mdata().bgposx" :bgposy="mdata().bgposy"/>
        <a href="#" class="message__btns">
          <svg width="24" height="19">
            <use xlink:href="#camera" ></use>
          </svg>
        </a>
      </div>
      <div class="message__content">Hey! So are we cool to meet at the art gallery? Say 8pm</div>
      <textarea name="response" class="message__response">Yeah that sounds great. See you then.</textarea>
      <Btn :takefull="true" class="message__replyBtn" bgc="#4EB7A8" bgcl="#28A290" title="REPLY"/>
    </form>
  </div>
</template>

<script>
//MAKE THE FORM GO AWAY WITH ANIMATION ON SUBMIT
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
    testSubmit(){}
  },
  mounted () {
    this.$refs.message.style.setProperty('--hovercol', this.bgc2)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
*
  margin 0
.message
  --hovercol pink
  min-width 290px
  width: 290px
  color white
  background-color #F2F2F2
  padding-bottom 25px
  &__top
    border-top-right-radius 3px
    border-top-left-radius 3px
    padding-top 22px
    padding-bottom 26px
    font-family "Open sans", sans-serif
    font-size 18px
    //
  &__midControls
    margin-top -47.5px
    fill #8e8d8d
    display flex
    justify-content space-between
    align-items flex-end
    padding 0 22px
  &__content
    margin 15px 22px
    padding 20px
    border-radius 5px
    color #868686
    background-color #fff
    font-size 13px
    font-weight 600
    position relative
    text-align left
    &:before
      content ''
      background-color #fff
      width 10px
      height 10px
      position absolute
      transform rotate(45deg)
      top -5px
      left calc(50% - 5px)
  &__response
    margin 0 22px
    margin-bottom 15px
    width calc(100% - 44px) !important
    resize none
    box-sizing border-box
    border 3px solid white
    background-color #E5E5E5
    border-radius 5px
    padding 17px
    font-size 13px
    font-weight 600
    font-family "Open Sans", sans-serif
    color #777777
  &__replyBtn
    margin 0 22px
.message__btns:hover
  fill var(--hovercol)

</style>