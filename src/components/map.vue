<template>
<div class="map__layout">

<div class="buttons__container">
  <button @click="setDate('')" type="button" class="date">Tutta la settimana</button>
  <div class="date__container">
    <button type="button" @click="setDate('2020-08-21')" class="date">21/08/2020</button>
    <button type="button" @click="setDate('2020-08-22')" class="date">22/08/2020</button>
    <button type="button" @click="setDate('2020-08-23')" class="date">23/08/2020</button>
    <button type="button" @click="setDate('2020-08-24')" class="date">24/08/2020</button>
    <button type="button" @click="setDate('2020-08-25')" class="date">25/08/2020</button>
    <button type="button" @click="setDate('2020-08-26')" class="date">26/08/2020</button>
    <button type="button" @click="setDate('2020-08-27')" class="date">27/08/2020</button>
    <button type="button" @click="setDate('2020-08-28')" class="date">28/08/2020</button>
  </div>
</div>

<div class="map__container">
  <l-map style="height: 600px; width: 100% " :zoom="zoom" :center="center">
    <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    <div v-for="marker in markers" :key="marker.longitude">
      <div v-if="marker.date==date">
        <l-marker :lat-lng="[marker.latitude , marker.longitude]"></l-marker>
      </div>
      <div v-else-if="date==''">
        <l-marker :lat-lng="[marker.latitude , marker.longitude]"></l-marker>
      </div>
    </div>
  </l-map>
</div>

</div>
</template>

<script>
import {LMap, LTileLayer, LMarker} from 'vue2-leaflet';
import { Icon } from 'leaflet';
import axios from 'axios'

delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
  iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
  iconUrl: require('leaflet/dist/images/marker-icon.png'),
  shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
});

export default {
  name: "Map",
  components: {
    LMap,
    LTileLayer,
    LMarker
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:'&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 2,
      center: [41, 13],
      date: '',
      markers: null
    };
  },
  mounted () {
    axios
      .get("https://cors-anywhere.herokuapp.com/https://storage.googleapis.com/public.storykube.com/start2impact/fires.json")
      .then(response => (this.markers = response.data))
      .catch(error => console.log(error))
  },
  methods: {
    setDate: function(date){
      this.date = date;
    }
  }
}
</script>

<style>

  /* Buttons */

  .buttons__container{
    padding: 25px;
    width: 100%;
  }

  .date__container{
    display: flex;
    justify-content: space-between;
    padding-top:  25px ;
  }

  .date{
    padding: 15px 30px;
    color: #000;
    background-color: #81B7FC;
    border: 3px solid #f1f1f1;
    border-radius: 25px;
    opacity: 0.9;
  }

  .date:hover{
    opacity: 1;
  }

  /* Map */

  .map__layout {
    padding: 25px 100px;
    display: flex;
    flex-wrap: wrap;
    max-width: 1250px;
    margin: 0 auto 80px auto;
}

  .map__container{
    width: 100%;
    max-width: 1250px;
    height: auto;
    margin: 0 auto;
    border: 3px solid #f1f1f1;
    box-shadow: 5px 10px 8px 10px #888888;
  }

</style>
