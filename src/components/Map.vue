<script>
import { Map, View } from 'ol';
import TileLayer from 'ol/layer/Tile';
import OSM from 'ol/source/OSM';
import { fromLonLat } from 'ol/proj';

export default {
  name: "Map",
  mounted() {
    new Map({
      target: 'map',
      layers: [
        new TileLayer({
          source: new OSM()
        })
      ],
      view: new View({
        center: fromLonLat([19.042563, 47.512841]),
        zoom: 13
      })
    });
  }
}
</script>

<template>
  <div id="map"></div>
</template>

<style scoped>
  #map {
    height: 100%;
  }
</style>
