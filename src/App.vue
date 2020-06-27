<template>
  <div id="app">
    <l-map ref="myMap" style="height:100vh" :zoom="zoom" :center= "center"> 
       <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
       <l-marker v-for="(station, index) in this.stationsLive":lat-lng="[station.lat, station.lon]" :key = "index" :icon="defaultIcon"></l-marker>
    </l-map>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {
  
  }, 
  data(){
    return {
      stationsLive: [],
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
  },
  methods: {
    fetchStationAvailability: function(){
      const urlPaths = ['station_status.json', 'station_information.json'];
      const requests = urlPaths.map(urlPath => fetch(`https://gbfs.urbansharing.com/edinburghcyclehire.com/${urlPath}`));
    Promise.all(requests)
    .then(responses => {
      responses.forEach(response => console.log(response.url, response.status))
      return responses;
     })
    .then(responses => Promise.all(responses.map(response => response.json())))
    .then(responses => this.mergeObjectsByStationID(responses[0].data.stations, responses[1].data.stations))
    .then(mergedResponses => this.stationsLive = mergedResponses)
    .then(setTimeout(this.fetchStationAvailability, 60000))
    },

    mergeObjectsByStationID: function(locationsArr, usageArr){
      const combinedArr = locationsArr.map((location) => {
        const matchingUsageObject = usageArr.find(stationUsage => Object.is(stationUsage.station_id, location.station_id))
        const merged = Object.assign(matchingUsageObject, location)
        return merged
      })
      return combinedArr
    }
  },
  mounted() {
      this.fetchStationAvailability();
      this.$nextTick(() => {
        this.$refs.myMap.mapObject;
      });
  }
}
</script>

<style>
body{
  margin: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0px;
}
#l-map {
  height: 1000px;
  width: 1000px;
}
</style>
