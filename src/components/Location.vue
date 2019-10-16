<template>
  <div class="loc" :style="locStyle">
    <div class="loc__map" id="map">
      <span class="loc__marker"></span>
    </div>
    <div class="loc__controls">
      <h3 class="loc__header"><a href="#">{{title}}</a></h3>
      <h5 class="loc__place">{{place}}</h5>
      <div class="wrapper">
        <button class="loc__routeBtn">X</button>
        <button class="loc__centerBtn">Y</button>
      </div>
    </div>
  </div>
</template>

<script>
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
  },
  mounted () {
    ymaps.ready(init);
    function init () {
      /**
       * Creating an instance of the map and binding it to the container
       * with the specified ID ("map").
       */
      var myMap = new ymaps.Map('map', {
          /**
           * When initializing the map, you must specify
           * its center and the zoom factor.
           */
          center: [55.76, 37.64], // Moscow
          zoom: 10,
          
          controls: []
      }, {}),
      myGeoObject = new ymaps.GeoObject({
            // The geometry description.
            geometry: {
                type: "Point",
                coordinates: [55.888, 37.888]
            },
            // Properties.
            properties: {
                // The placemark content.
                iconContent: '',
                hintContent: ''
            }
        }, {
            /**
             * Options.
             * The placemark's icon will stretch to fit its contents.
             */
            preset: 'islands#blackStretchyIcon',
            iconLayout: 'default#imageWithContent',
            // Custom image for the placemark icon.
            iconImageHref: require('./../assets/img/mapMarker.svg'),
            // The size of the placemark.
            iconImageSize: [34, 45],
            // The placemark can be dragged.
            draggable: false
        })
        let myPlacemark = new ymaps.Placemark(myMap.getCenter(), {
            hintContent: 'A custom placemark icon',
            balloonContent: 'This is a pretty placemark'
        }, {
            /**
             * Options.
             * You must specify this type of layout.
             */
            iconLayout: 'default#image',
            // Custom image for the placemark icon.
            iconImageHref: require('./../assets/img/mapMarker.svg'),
            // The size of the placemark.
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

.loc__map
  height 200px
.loc__controls
  display flex
  height 70px
  box-sizing border-box
  align-items center

.loc__header
  flex 1 0 0
  font-size 30px
  font-weight 300
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
  outline 1px dashed yellow
</style>