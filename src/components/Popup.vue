<template>
  <l-popup>
      <div id="bike-status">
        <h3>{{station.name}}</h3>
        <div class = "availability">
            <div class="logo_wrapper">
                <img src="../assets/icons/bike.svg" alt="Logo of bicycle" width="30" height="30">
            </div>
            <span>{{station.num_bikes_available}}</span>
        </div>
        <div class = "availability">
            <div class="logo_wrapper--rack">
                <img src="../assets/icons/rack.svg" alt="Logo of bike rack" width="30" height="30">
            </div>
            
            <span>{{station.num_docks_available}}</span>
        </div>
      </div>    
    </l-popup>
</template>

<script>
export default {
    name: "popup",
    props: ['station']


}
</script>

<style scoped>

h3{
    margin-bottom: 8px;
}
.logo_wrapper{
    
    width:40px;
    height: 40px;
    justify-content: center;
    align-items: center;
    display: flex;
    background-color: #FEE440;
    border-radius:50%;
    box-shadow:  .1rem .40rem .45rem 0 rgba(100,110,140,.4);
    margin-right: 5px;

}
.logo_wrapper--rack{
    margin-top: 8px;
     width:40px;
    height: 40px;
    justify-content: center;
    align-items: center;
    display: flex;
    background-color: #87ffc2;
    border-radius:50%;
    box-shadow:  .1rem .40rem .45rem 0 rgba(100,110,140,.4);
    margin-right: 5px;
}
span {
    font-weight: bold;
}
#bike-status{
    color: grey;
}

.availability{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items:center;
}

.availability span{
    font-size: 15px;
}
</style>