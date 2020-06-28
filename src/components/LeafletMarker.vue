<template>
    <l-marker :lat-lng="[station.lat, station.lon]">
          <l-icon  :icon-size="[100,100]" :icon-url="customMarker"></l-icon>
    </l-marker>    
        

</template>

<script>

import customMarker from '../assets/icons/station.svg'  //this is to byepass leaflet-2-vue bug 

export default {
    name: "leaflet-marker", 
    props: ['station'],
    data(){
      return {
        customMarker, //this is to byepass leaflet-2-vue bug 
        staticAnchor: [16, 37],
        }
    },    
}
</script>

<style>

</style>