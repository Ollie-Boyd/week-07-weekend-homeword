<template>
  <div id="app">
    <leaflet-map :stationsLive="stationsLive"></leaflet-map>
  </div>
</template>

<script>

import LeafletMap from "./components/LeafletMap";


export default {
  name: 'App',
  components: {
    "leaflet-map": LeafletMap
  
  }, 
  data(){
    return {
      stationsLive: []
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
