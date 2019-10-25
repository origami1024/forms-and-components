<template>
  <div class="video" :style="wrapStyle" >
    <video controls width=100%>
      <source src="./../assets/vids/bunny.webm" type="video/webm">
      Sorry, browser does not support
    </video>
  </div>
</template>

<script>
export default {
  name: 'Video',
  props: {
    vSrc: {type: String, default: ''},
    bgc: {type: String, default: 'blue'},
  },
  data: function() {
    return {
    }
  },
  computed: {
    wrapStyle() {
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
.video
  border 1px solid black

  
</style>