<template>
    <l-marker :lat-lng="[station.lat, station.lon]">
          <l-icon  :icon-size="[40,100]" :icon-url="WhichIcon"></l-icon>
    </l-marker>    
</template>

<script>

import customMarkerStation from '../assets/icons/station.svg'  //this is to byepass leaflet-2-vue bug 
import customMarkerStationEmpty from '../assets/icons/station--no-bikes.svg'  //this is to byepass leaflet-2-vue bug 

export default {
    name: "leaflet-marker", 
    props: ['station'],
    data(){
      return {
        customMarkerStation, 
        customMarkerStationEmpty,//this is to byepass leaflet-2-vue bug 
        staticAnchor: [16, 37],
        }
    },
    computed:{
        WhichIcon() {
        return (Object.is(this.station.num_bikes_available, 0) ? this.customMarkerStationEmpty : this.customMarkerStation)
      }
    }
}
</script>

<style>

</style>