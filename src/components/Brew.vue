<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-info">Breweries List</h1>
      </div>
      <!-- /.col-12 -->
    </div>

    <div class="row">
      <div class="col-6">
        <!-- {{brews}} -->
        <BrewList
          @mouse-over-brew="mouseOverBrew"
          @mouse-left-brew="mouseLeftBrew"
          v-bind:brews="brews" />
      </div>
      <div class="col-6">
        <!-- insert map here -->
        <BrewMap v-bind:brews="brews" />
      </div>
    </div>
    <!-- /.row -->
  </div>
</template>

<script>
import axios from 'axios'
import BrewList from './BrewList.vue'
import BrewMap from './BrewMap.vue'

export default {
  name: 'Brew',
  components: {
    BrewList,
    BrewMap
  },
  data() {
    return {
      brews: []
    }
  },
  mounted() { // this means that we are waiting for the component to mount. We it is done, we are making an axios call to the brewery db and we assign the result of that call to the data property "brews". We then use v-for directive to loop through the array items. We are also binding the index which is actually a key within the "brews" array to track down the list items 
    // https://api.openbrewerydb.org/breweries
    // console.log('mounted');
    axios.get('https://api.openbrewerydb.org/breweries')
      // .then(res => console.log(res)) - we take the entire response
      // .then(res => console.log(res.data)) - we take only the response body
      // .catch(err => console.log(err));
      //.then(res => this.brews = res.data)
      .then(res => this.brews = res.data.filter(res => res.state == "Arizona"))
      .catch(err => console.log(err));
  },
  methods: {
    mouseOverBrew(index) {
      console.log(index + 'mouse-over-brew');
      // marker.bindPopup("<b>" + brew.name + "</b><p>Velos disponibles: " + brew.street + "</p><p>Velos totales: " + brew.state + "</p>").openPopup();
    },
    mouseLeftBrew(index) {
      console.log(index + 'mouse-left-brew');
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  
</style>
