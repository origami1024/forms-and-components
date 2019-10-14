<template>
  <div class="loc" :style="locStyle">
    <div class="loc__map" id="map">
      <span class="loc__marker"></span>
    </div>
    <div class="loc__controls">
      <h3 class="loc__header">{{title}}</h3>
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
                coordinates: [55.8, 37.8]
            },
            // Properties.
            properties: {
                // The placemark content.
                iconContent: 'I\'m draggable',
                hintContent: 'Come on, drag already!'
            }
        }, {
            /**
             * Options.
             * The placemark's icon will stretch to fit its contents.
             */
            preset: 'islands#blackStretchyIcon',
            // The placemark can be dragged.
            draggable: false
        })
      myMap.geoObjects.add(myGeoObject)
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
.loc__header
  flex 1 0 0
.loc__place
  flex 1 0 0
.wrapper
  flex 2 0 0
  display flex
  justify-content flex-end
  outline 1px dashed yellow
</style>