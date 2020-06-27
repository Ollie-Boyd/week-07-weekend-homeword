<template>
  <l-map ref="myMap" style="height:100vh" :zoom="zoom" :center= "center"> 
       <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
       <l-marker v-for="(station, index) in this.stationsLive" :lat-lng="[station.lat, station.lon]" :key="index" :icon="defaultIcon"></l-marker>
    </l-map>
</template>

<script>
export default {
    name: "leaflet-map",
    props: ['stationsLive'],
    data(){
    return {
      url: "http://{s}.tile.osm.org/{z}/{x}/{y}.png",
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 13,
      center: [55.950191, -3.187550],
      defaultIcon: L.icon({
        iconUrl: 'http://leafletjs.com/examples/custom-icons/leaf-green.png',
        shadowUrl: 'http://leafletjs.com/examples/custom-icons/leaf-shadow.png',
        iconSize:     [38, 95],
        shadowSize:   [50, 64],
        iconAnchor:   [22, 94],
        shadowAnchor: [4, 62],
        popupAnchor:  [-3, -76]
      })
    }
  }
}
</script>

<style>

</style>