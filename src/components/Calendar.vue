<template>
  <div class="calendar" :style="{'--bgc': bgc}">
    <div class="calendar__top" :style="headerStyle">
      <p class="calendar__header">{{date.getDate()}}</p>
      <div class="calendar__monthControl">
        <ArrBtn :style="{border: 0}" bgc="white" hoverColor="#ffffff33"/>
        {{getMonth}}
        <ArrBtn :dir="false" :style="{border: 0}" bgc="white" hoverColor="#ffffff33"/>
      </div>
    </div>
      <div class="calendar__dayControl">
        <table class="calendar__table" width="100%">
          <tr class="calendar__tableHeader" :style="thStyle">
            <th class="calendar__cell" v-for="item in weekDays" :key="item">{{item}}</th>
          </tr>
          <!-- HERE GOES 7tr each containing 5 td -->
          <tr v-for="item in 5" :key="item">
            <td class="calendar__cell calendar__daycell" v-for="subitem in 7" :key="subitem" :class="{currentDay: ((subitem + 1) + ((item - 1) * 7)) === generateTable[generateTable.length-3], secondaryDay: ((subitem + ((item - 1) * 7) < generateTable[generateTable.length-2]) || ((subitem + 1) + ((item - 1) * 7)>generateTable[generateTable.length-1]))}">{{generateTable[(subitem - 1) + ((item - 1) * 7)]}}</td>
          </tr>
        </table>
      </div>
    <div class="calendar__footer">TODAY</div>
  </div>
</template>

<script>
//do a table with table head as weekdays
//change word in the footer
//
//CLICKABLE MONTH ARROWS
//CLICKBALE DAYS IN TABLE
import ArrBtn from './ArrBtn.vue'
export default {
  name: 'Calendar',
  props: {
    date: {type: Date, default: new Date()},
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
      months: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
      weekDays: ["MON", "TUE", "WED", "THU", "FRI", "SAT", "SUN"],
      table: []
    }
  },
  computed: {
    generateTable() {
      let date = this.date
      let tmpTable = []
      let lastDayOfThisMonth = new Date(date.getFullYear(), date.getMonth()+1, 0).getDate()
      console.log(lastDayOfThisMonth)
      for (let i=1; i<=lastDayOfThisMonth; i++) {
        tmpTable.push(i)
      }
      let firstWeekDayOfMonth = new Date(date.getFullYear(), date.getMonth(), 1).getDay()
      let lastDayOfPrevMonth = new Date(date.getFullYear(), date.getMonth(), 0).getDate()
      
      for (let index = 0; index < firstWeekDayOfMonth - 1; index++) {
        tmpTable.unshift(lastDayOfPrevMonth - index)
      }
      for (let i=1; i<=7; i++) {
        tmpTable.push(i)
      }
      tmpTable.push(firstWeekDayOfMonth + date.getDate())
      tmpTable.push(firstWeekDayOfMonth)
      tmpTable.push(lastDayOfThisMonth + firstWeekDayOfMonth)
      return tmpTable
    },
    getMonth() {
      return this.months[this.date.getMonth()]
    },
    headerStyle() {
      return `
      background-color: ${this.bgc};
      `
    },
    thStyle() {
      return `
      background-color: ${this.bgc};
      border: 1px solid ${this.bgc};
      `
    }
    
  },
  components: {
    ArrBtn
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
.calendar
  --bgc pink
  border-radius 3px
  min-width 270px
  &__top
    color #fff
  &__header
    font-size 80px
    font-family "Open Sans"
  &__monthControl
    background-color #D54C2C
    font-size 24px
    padding 8px 0
    display flex
    justify-content space-between
    align-items center
  &__dayOfWeekLabel
    display flex
    color white
    justify-content space-between //maybe do it some other way - to place it on top of columns
  &__footer
    background-color #E5E5E5
    font-size 13px
    color #868686
    font-family "Open Sans"
    font-weight 600
    padding 20px
    text-align left

.calendar__table
  //table-layout fixed
  border-collapse separate
  border-spacing 0px
  border-bottom 1px solid white
.calendar__tableHeader
  border 2px solid black
  font-size 9px
.calendar__cell
  width calc(100% / 7)
  color white
  padding 9px
.calendar__daycell
  background-color #F2F2F2
  border-left 1px solid white
  border-top 1px solid white
  font-size 20px
  color #868686
  cursor pointer
  &:hover
    outline 2px solid black
    color black
  &:last-child
    border-right 1px solid white
.secondaryDay
  color white
  font-size 18px  
.currentDay
  color #fff
  background-color var(--bgc)

</style>