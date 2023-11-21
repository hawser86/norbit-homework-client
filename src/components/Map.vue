<script>
import { Feature, Map, View } from 'ol';
import TileLayer from 'ol/layer/Tile';
import OSM from 'ol/source/OSM';
import { fromLonLat } from 'ol/proj';
import { Fill, RegularShape, Stroke, Style } from 'ol/style';
import { LineString, Point } from 'ol/geom';
import VectorLayer from 'ol/layer/Vector';
import VectorSource from 'ol/source/Vector';

export default {
  name: "Map",
  props: {
    boatTrack: Array
  },
  data: () => ({
    source: new VectorSource()
  }),
  watch: {
    boatTrack: {
      handler() {
        this.refreshBoatTrack();
      },
      deep: true
    }
  },
  methods: {
    refreshBoatTrack() {
      this.source.clear();
      this.source.addFeatures([this.createTriangle(this.boatTrack[this.boatTrack.length - 1])]);

      const lines = this.boatTrack
          .slice(0, -1)
          .map((position, index) => this.createLine(position, this.boatTrack[index + 1]));
      this.source.addFeatures(lines);
    },
    createTriangle({ latitude, longitude, heading }) {
      const stroke = new Stroke({ color: 'black', width: 2 });
      const fill = new Fill({ color: 'red' });
      const style = new Style({
        image: new RegularShape({
          fill: fill,
          stroke: stroke,
          points: 3,
          radius: 10,
          rotation: (Math.PI / 180) * heading,
          scale: [0.5, 1]
        }),
      });

      const feature = new Feature(new Point(fromLonLat([longitude, latitude])));
      feature.setStyle(style);

      return feature;
    },
    createLine(from, to) {
      const stroke = new Stroke({ color: 'red', width: 2 });
      const style = new Style({
          stroke: stroke,
      });

      const points = [fromLonLat([from.longitude, from.latitude]), fromLonLat([to.longitude, to.latitude])];
      const feature = new Feature({
        geometry: new LineString(points)
      });
      feature.setStyle(style);

      return feature;
    }
  },
  mounted() {
    this.refreshBoatTrack();

    const vectorLayer = new VectorLayer({
      source: this.source,
    });

    new Map({
      target: 'map',
      layers: [
        new TileLayer({
          source: new OSM()
        }),
        vectorLayer
      ],
      view: new View({
        center: fromLonLat([20.73998593, 48.21339894]),
        zoom: 16
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
