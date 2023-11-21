<script>
import { io } from 'socket.io-client';
import Map from './components/Map.vue';

export default {
  name: 'App',
  components: { Map },
  data: () => ({
    boatPosition: { latitude: 0, longitude: 0, heading: 0 }
  }),
  mounted() {
    const socket = io("http://localhost:9876");

    socket.on('boat-position', position => {
      this.boatPosition = position;
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
      <Map :boat-position="boatPosition"></Map>
    </div>

    <div class="row footer">
      footer...
    </div>
  </div>
</template>

<style scoped>
.box {
  display: flex;
  flex-flow: column;
  height: 100%;
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
