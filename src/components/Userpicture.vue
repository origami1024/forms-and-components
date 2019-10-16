<template>
  <div class="userpicture" :style="imgStyle"></div>
</template>

<script>
export default {
  name: 'Userpicture',
  props: {
    img: {type: String, default: './../assets/img/john.png' },
    bgposx: {type: Number, default: -25},
    bgposy: {type: Number, default: 0},
  },
  data: function() {
    return {
    }
  },
  computed: {
    imgStyle() {
      return `
      background-image: url(${this.img});
      background-position: ${this.bgposx}px ${this.bgposy}px;
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
.userpicture
  width 85px
  height 85px
  border-radius 100%
  border 5px solid #E5E5E5
  
</style>