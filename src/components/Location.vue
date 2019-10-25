<template>
  <div class="loc" :style="locStyle">
    <div class="loc__map" id="map">
      <span class="loc__marker"></span>
    </div>
    <div class="loc__controls">
      <h3 class="loc__header"><a href="#">{{title}}</a></h3>
      <h5 class="loc__place">{{place}}</h5>
      <div class="wrapper">
        <button class="loc__btn loc__routeBtn" @click="makeRoute">
          <svg width="20" height="27">
            <use xlink:href="#mapPin" ></use>
          </svg>
        </button>
        <button class="loc__btn loc__centerBtn" @click="positionSelf">
          <svg width="29" height="30">
            <use xlink:href="#mapMyLoc" ></use>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
let
  myMap = undefined,
  markerPos = [44.98, 34.14],
  ownPos = undefined,
  destTitle = 'some'
//TODO: need to clean the code a bit
//make captions for the buttons
//rethink the placemarker, it needs caption
//figure out how to access data variables from inside functions - dont use globals


//there is yandex-api script added to the head in the main.html
//todo
//mapMarker shade
//style buttons
//route button
//my location button
export default {
  name: 'Loc',
  props: {
    title: {type: String, default: 'Meet us!'},
    place: {type: String, default: '1259 CALIFORNIA ST SAN FRANCISCO, CA'},
    bgc: {type: String, default: 'blue'}
  },
  data: function() {
    return {
      
    }
  },
  computed: {
    locStyle() {
      return `
      background-color: ${this.bgc};
      color: white;
      font-family: 'Open Sans';
      `
    }
  },
  methods: {
    positionSelf(){
      ymaps.geolocation.get({
        provider: 'browser',
        mapStateAutoApply: true
      }).then(function (result) {
        result.geoObjects.options.set('preset', 'islands#blueCircleIcon')
        myMap.geoObjects.add(result.geoObjects);
        console.log(result.geoObjects.position)
        setTimeout(function () {
          ownPos = result.geoObjects.position  
        }, 5);
      });
    },
    makeRoute(){
      if (ownPos !== undefined) {
        ymaps.route([
          ownPos,
          markerPos
        ]).then(function (route) {
          myMap.geoObjects.add(route);
          var points = route.getWayPoints(),
          lastPoint = points.getLength() - 1;
          points.options.set('preset', 'islands#redStretchyIcon');
          // Setting the placemark content in the start and end points.
          points.get(0).properties.set('iconContent', 'You are here');
          points.get(lastPoint).properties.set('iconContent', destTitle);
          }, function (error) {
            alert('An error occurred: ' + error.message);
          })
      } else { alert(ownPos) }
      
    }
  },
  mounted () {
    destTitle = this.place
    ymaps.ready(init)
    function init () {
      /**
       * Creating an instance of the map and binding it to the container
       * with the specified ID ("map").
       */
      let geolocation = ymaps.geolocation
      myMap = new ymaps.Map('map', {
          center: markerPos,
          zoom: 9,  
          controls: []
        }, {})
      // myMap.behaviors.disable('scrollZoom')
      // myMap.controls.add('zoomControl', {
      //   size: "small",
      //   position: []
      // });
      let myPlacemark = new ymaps.Placemark(myMap.getCenter(), {
          hintContent: 'A custom placemark icon',
          balloonContent: 'This is a pretty placemark'
      }, {
          iconLayout: 'default#image',
          // Custom image for the placemark icon.
          iconImageHref: require('./../assets/img/mapMarker.svg'),
          iconImageSize: [34, 45],
          /**
            * The offset of the upper left corner of the icon relative
            * to its "tail" (the anchor point).
            */
          iconImageOffset: [-18, -45]
      })
      myMap.geoObjects.add(myPlacemark)
      
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
*
  margin 0
svg
  fill white
.loc__map
  height 200px
.loc__controls
  display flex
  height 70px
  box-sizing border-box
  align-items center
  padding 0 25px

.loc__header
  flex 1 0 0
  font-size 30px
  font-weight 300
  padding 0
  margin 0
  & a
    color white
    text-decoration none
.loc__place
  flex 1 0 0
  font-size 13px
.wrapper
  flex 2 0 0
  display flex
  justify-content flex-end
.loc__btn
  border 0
  background-color transparent
  cursor pointer
  margin-left 20px
  padding 0
</style>