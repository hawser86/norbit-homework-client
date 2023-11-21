<script>
import Map from './components/Map.vue';

export default {
  name: 'App',
  components: { Map }
}
</script>

<template>
  <div class="box">
    <div class="row header">
      <h1>Boat position</h1>
    </div>

    <div class="row content">
      <Map></Map>
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
