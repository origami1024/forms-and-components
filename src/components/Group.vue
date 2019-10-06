<template>
  <section class="group">
    <h2>{{title.toUpperCase()}}</h2>
    <div class="group__display">
      <slot></slot>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Group',
  props: {
    title: {type: String, default: 'new group'}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
.group
  text-align center
  outline 2px dashed lime
  font-family Raleway, sans-serif
  padding 10px 0

.group__display
  outline 2px dashed pink
  padding 5px 0

</style>