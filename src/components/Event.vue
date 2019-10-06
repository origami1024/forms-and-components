<template>
  <div class="event" :style="wrapStyle">
    <img class="event__img" :src="model.img" :alt="model.alt">
    <div class="event__main">
      <h2 class="event__header" :class="{'event__header--calendar': calendar}">{{model.title}}</h2>
      <p class="event__date" :class="{'event__date--calendar': calendar}">
        <span :class="{'event__date-calendar--day': calendar}">{{model.date.getDate()}} </span>
        <span :class="{'event__date-calendar--month': calendar}">{{monthValue}} </span>
        <span v-show="!calendar">{{model.date.getFullYear()}}</span>
      </p>
      <p class="event__text">{{model.text}}</p>
      <div class="btnwrap">
        <Btn class="event__btn_add" title="ADD TO GALERY" :bgc="model.bgc2" :bgcl="model.bgc2" v-show="calendar" :w="129" :small="true"/>
      </div>
      
      <!-- <button v-show="calendar" class="event__btn_add" :style="addbtnStyle">ADD TO CALENDAR</button> -->
    </div>
  </div>
</template>

<script>
import Btn from './Btn.vue'
export default {
  name: 'Event',
  components: {
    Btn
  },
  props: {
    calendar: {type: Boolean, default: false},
    model: {type: Object, default: {title:'1', date:new Date(2010, 9, 30), text:'1', bgc:'blue', bgc2: 'pink', img: './../assets/img/event1.png', alt: 'default alt text'}},
  },
  data: function() {
    return {
      months: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
    }
  },
  computed: {
    monthValue() {
      return this.calendar ? this.months[this.model.date.getMonth()].substring(0,3) : this.months[this.model.date.getMonth()].toUpperCase()
    },
    wrapStyle() {
      return `
      background-color: ${this.model.bgc};
      `
    },
    addbtnStyle() {return `border-bottom: 3px solid ${this.model.bgc2}; color: ${this.model.bgc2};`}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.event
  color white
  border-radius 3px
  display flex
  overflow hidden
  font-family 'Raleway'
  &__img
    max-width 100%
    min-width 1%
    height 234px
    flex 2 0 0
    align-self flex-start
  &__main
    flex 3 0 0
    padding 0 20px
    padding-top 25px
    text-align left
    display flex
    flex-direction column
  &__header
    font-size 24px
    line-height 0.93
    margin 0
    color #ffffff
  &__date
    font-size 11px
    margin 15px 0
    font-family 'Open sans'
  &__text
    margin 0
    margin-bottom 18px
    font-size 10px
    line-height 1.2
    letter-spacing 0.5px
    order 3
    
.event__date--calendar
  order 1
.event__header--calendar
  order 2
  font-size 13px
  margin-bottom 8px
.event__date-calendar--day
  font-size 70px
  line-height 0.36
.event__date-calendar--month
  font-size 30px
  line-height 0.87

.btnwrap
  height 22px
  display flex
  order 4
</style>