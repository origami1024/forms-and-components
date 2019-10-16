<template>
  <div class="uprofile" ref="uprofile">
    <Userpicture class="uprofile__img" :img="udata().img" :bgposx="udata().bgposx" :bgposy="udata().bgposy"/>
    <div class="uprofile__detail">
      <h2 class="uprofile__uname">{{udata().uname}}</h2>
      <h4 class="uprofile__utitle">{{udata().utitle}}</h4>
      <div class="uprofile__smedia">
        <a :href="'#'+udata().fb" class="uprofile__smlink">
          <svg width="25" height="21">
            <use class="fb" xlink:href="#icons8-fb" ></use>
          </svg>
        </a>
        <a :href="'#'+udata().tt" class="uprofile__smlink">
          <svg width="25" height="21">
            <use class="tt" xlink:href="#icons8-tt" ></use>
          </svg>
        </a>
        <a :href="'#'+udata().bb" class="uprofile__smlink">
          <svg width="25" height="21">
            <use class="bb" xlink:href="#icons8-bb" ></use>
          </svg>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import Userpicture from './Userpicture.vue'
export default {
  name: 'Userprofile',
  props: {
    udata: {type: Function, default: function() {return{
        uname: "John Smith",
        utitle: "UX Designer",
        fb: '111',
        tt: '222',
        ll: '333',
        img: require('./../assets/img/john.png'),
        bgposx: '-25px',
        bgposy: '0',
    }}},
    bgc: {type: String, default: 'blue'},
    bgc2: {type: String, default: 'red'},
  },
  data: function() {
    return {
    }
  },
  components: {
    Userpicture
  },
  computed: {
  },
  methods: {
    
  },
  mounted () {
    this.$refs.uprofile.style.setProperty('--hovercol', this.bgc2)
    this.$refs.uprofile.style.setProperty('--bgc', this.bgc)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
*
  margin 0

.uprofile
  --hovercol pink
  --bgc blue
  display flex
  margin 25px 0
  color #4F4F4F
  &__uname
    font-size 18px
    color var(--hovercol)
  &__utitle
    font-size 11px
    margin-bottom 11px
    color #4F4F4F
  &__smedia
    display flex
    justify-content space-evenly
  &__smlink
    display inline-block
    min-width 25px
    max-width 25px
    max-height 21px
    min-height 21px
    background-size 100% 100%
    &:hover
      fill var(--hovercol)
  &__detail
    display flex
    flex-direction column
    justify-content space-between
    width 170px
    height 95px
    box-sizing border-box
    padding-top 12px
    padding-bottom 15px
    background-repeat no-repeat
    border-radius 7px
    background-color #E5E5E5
    margin-left 15px
    position relative
    z-index 2
    cursor pointer
    fill #757575
    transition-duration .3s
    &:hover
      color white
      fill white
      background-color var(--bgc)
      &:before
        background-color var(--bgc)
    &:before
      content ''
      width 10px
      height 10px
      background-color #e5e5e5
      position absolute
      left -5px
      top calc(50% - 5px)
      transform rotate(45deg)
      border-radius 3px
      z-index 1
      transition-duration .3s
.uprofile__detail:hover>.uprofile__uname
  color white
  
.uprofile__detail:hover>.uprofile__utitle
  color white

</style>