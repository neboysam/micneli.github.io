<template>
  <div class="row map">
    <!-- <h2>Center is {{currentCenter}}, zoom is at {{currentZoom}}</h2> -->
    <l-map
      @update:zoom="zoomUpdate"
      @update:center="centerUpdate"
      :zoom="zoom"
      :center="center">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-marker
        v-bind:key="index"
        v-for="(brew, index) in brews"
        :lat-lng="latLng(brew.latitude, brew.longitude)">
        <!-- <l-popup>
          {{brew.name}},<br> {{brew.street}},<br> {{brew.state}}
        </l-popup>           -->
      </l-marker>
    </l-map>
  </div>
  <!-- /.row map --> 
</template>

<script>
import L from 'leaflet';
import { LMap, LTileLayer, LMarker} from 'vue2-leaflet'; // LPopup

export default {
  name: "BrewMap",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    // LPopup
  },
  props: {
    brews: Array
  },
  data() {
    return{
      zoom: 6,
      center: L.latLng(32.635304, -112.631836),
      currentCenter: L.latLng(32.635304, -112.631836),
      currentZoom: 6,
      url:'https://tile.thunderforest.com/transport/{z}/{x}/{y}.png?apikey=b82c7c65d0734b6689824d32e216bc74',
      attribution:'&copy; <a href="https://www.thunderforest.com">Thunderforest</a> contributors',
      marker: L.latLng(32.635304, -112.631836),
    }
  },
  methods: {
    latLng(lat, lng) {
      return L.latLng(lat, lng);
    },
    centerUpdate(center) {
      this.currentCenter = center
    },
    zoomUpdate(zoom) {
      this.currentZoom = zoom
    }
  }
}
</script>

<style scoped>
  .map {
    height: 95vh;
  }
</style>