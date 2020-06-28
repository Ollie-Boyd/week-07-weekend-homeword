<template>
  <l-marker :lat-lng="[station.lat, station.lon]">
    <l-icon  :icon-size="[40,40]" :popupAnchor="popupAnchor"  :icon-url="WhichIcon"></l-icon>
    <popup :station="station"></popup>
  </l-marker>    
</template>

<script>

import customMarkerStation from '../assets/icons/station.svg'  //this is to byepass leaflet-2-vue bug https://stackoverflow.com/questions/50864855/vue-js-leaflet-marker-is-not-visible
import customMarkerStationEmpty from '../assets/icons/station--no-bikes.svg'  //this is to byepass leaflet-2-vue bug 
import Popup from './Popup.vue'

export default {
    name: "leaflet-marker", 
    props: ['station'],
    data(){
      return {
        customMarkerStation, 
        customMarkerStationEmpty,//this is to byepass leaflet-2-vue bug 
        // staticAnchor: [20, 40],  // [x, y] in pixels https://stackoverflow.com/questions/46101450/explanation-of-leaflet-custom-icon-latlng-vs-xy-coordinates
        popupAnchor: [1, -18],
        }
    },
    computed:{
      WhichIcon() {
      return (Object.is(this.station.num_bikes_available, 0) ? this.customMarkerStationEmpty : this.customMarkerStation)
      }
    },
    components: {
      "popup": Popup,
    }
}
</script>

<style>


</style>