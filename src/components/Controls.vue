<script>
import ToggleSwitch from "./ToggleSwitch.vue";

export default {
  name: "Controls",
  components: { ToggleSwitch },
  props: {
    isRecordingRunning: Boolean,
    selectedTrackId: Number,
    trackList: []
  },
  emits: ['update:isRecordingRunning', 'update:selectedTrackId', 'loadTrack']
}
</script>

<template>
  <div class="container">
    <div class="block">
      <h3>Record</h3>
    </div>
    <div class="block">
      <ToggleSwitch
          :model-value="isRecordingRunning"
          @update:model-value="$emit('update:isRecordingRunning', $event)"
      ></ToggleSwitch>
    </div>

    <div class="block">
      <h3>Recordings</h3>
    </div>
    <div class="block">
      <select :value="selectedTrackId" @change="$emit('update:selectedTrackId', Number($event.target.value))">
        <option v-for="track in trackList" :value="track.id">
          {{ track.name }}
        </option>
      </select>
    </div>
    <div class="block">
      <button @click="$emit('loadTrack')">Load track</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: table;
}
.block {
  padding: 0 20px 0 0;
  display: table-cell;
  vertical-align: middle;
}
</style>