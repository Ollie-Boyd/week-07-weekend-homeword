<template>
  <l-map ref="myMap" style="height:100vh" :zoom="zoom" :center= "center"> 
    <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    <leaflet-marker v-for="(station, index) in this.stationsLive" :station="station" :key ="index"></leaflet-marker>

  </l-map>
</template>

<script>
// import customMarker from '../assets/icons/station.svg'
import LeafletMarker from "./LeafletMarker.vue"

export default {
    name: "leaflet-map",
    props: ['stationsLive'],
    computed: {
      
    },
    data(){
      return {
        // customMarker,
        url: "http://{s}.tile.osm.org/{z}/{x}/{y}.png",
        attribution:
          '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
        zoom: 13,
        center: [55.950191, -3.187550],
        staticAnchor: [16, 37],
     
      
      }
    },
    components: {
     "leaflet-marker": LeafletMarker
    },
    mounted(){
      console.log(this.$refs.myMap.mapObject.getZoom())
    }
}
</script>

<style>




</style>