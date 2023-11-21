<script>
import { io } from 'socket.io-client';
import Map from './components/Map.vue';
import Controls from './components/Controls.vue';

export default {
  name: 'App',
  components: { Map, Controls },
  data: () => ({
    boatPath: [],
    isRecordingRunning: false,
    socket: io("http://localhost:9876")
  }),
  methods: {
    updateRecordingStatus() {
      this.socket.emit('update-recording-status', this.isRecordingRunning);
    }
  },
  mounted() {
    this.socket.on('boat-position', position => {
      this.boatPath = [position.position];
    });

    this.socket.on('update-recording-status', isRecordingRunning => {
      this.isRecordingRunning = isRecordingRunning;
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
      <Map :boat-path="boatPath"></Map>
    </div>

    <div class="row footer">
      <Controls
          v-model:is-recording-running="isRecordingRunning"
          @update:is-recording-running="updateRecordingStatus()"
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
