<script>
import Map from './components/Map.vue';
import { io } from 'socket.io-client';

export default {
  name: 'App',
  components: { Map },
  data: () => ({
    dummyBoatPosition: {
      latitude: 48.21339894,
      longitude: 20.73998593,
      heading: 3.470315226
    }
  }),
  mounted() {
    const socket = io("http://localhost:9876");
  }
}
</script>

<template>
  <div class="box">
    <div class="row header">
      <h1>Boat position</h1>
    </div>

    <div class="row content">
      <Map :boat-position="dummyBoatPosition"></Map>
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
