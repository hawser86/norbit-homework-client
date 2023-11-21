<script>
import { io } from 'socket.io-client';
import Map from './components/Map.vue';
import Controls from './components/Controls.vue';

export default {
  name: 'App',
  components: { Map, Controls },
  data: () => ({
    boatTrack: [],
    isRecordingRunning: false,
    socket: io("http://localhost:9876"),
    trackList: [],
    selectedTrack: null
  }),
  methods: {
    updateRecordingStatus() {
      this.socket.emit('update-recording-status', this.isRecordingRunning);
    },
    loadTrack() {
      this.socket.emit('load-track', this.selectedTrack);
    }
  },
  mounted() {
    this.socket.on('boat-position', boatData => {
      if (boatData.shouldRecord) {
        this.boatTrack.push(boatData.position);
      } else {
        this.boatTrack = [boatData.position];
      }
    });

    this.socket.on('update-recording-status', isRecordingRunning => {
      this.isRecordingRunning = isRecordingRunning;
    });

    this.socket.on('track-list', trackList => {
      this.trackList = trackList;
    });
  }
}
</script>

<template>
  <div class="box">
    <div class="row header">
      <h1>Boat position</h1>
    </div>

    <div class="row content">
      <Map :boat-track="boatTrack"></Map>
    </div>

    <div class="row footer">
      <Controls
          v-model:is-recording-running="isRecordingRunning"
          @update:is-recording-running="updateRecordingStatus()"
          :track-list="trackList"
          v-model:selected-track="selectedTrack"
          @load-track="loadTrack()"
      ></Controls>
    </div>
  </div>
</template>

<style scoped>
.box {
  display: flex;
  flex-flow: column;
  height: 100%;
}

.box .row {
  margin-bottom: 10px;
}

.box .row.header {
  flex: 0 1 auto;
}

.box .row.content {
  flex: 1 1 auto;
}

.box .row.footer {
  flex: 0 1 40px;
}
</style>
