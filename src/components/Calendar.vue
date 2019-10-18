<template>
  <div class="calendar">
    <div class="calendar__header" :style="headerStyle">
      <p>24</p>
      <div class="calendar__monthControl">
        1
        Septembre
        3
      </div>
    </div>
      <div class="calendar__dayControl">
        <div class="calendar__dayOfWeekLabel">
          1234567
        </div>
        <div class="calendar__daysTable">
          7x5
        </div>
      </div>
    <div class="calendar__footer">TODAY</div>
  </div>
</template>

<script>
export default {
  name: 'Calendar',
  props: {
    title: {type: String, default: 'BUTTON'},
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    headerStyle() {
      return `
      background-color: ${this.bgc};
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
.calendar
  border-radius 3px
  min-width 270px
  
</style>