<script>
import ToggleSwitch from "./ToggleSwitch.vue";

export default {
  name: "Controls",
  components: { ToggleSwitch },
  props: {
    isRecordingRunning: Boolean
  },
  emits: ['update:isRecordingRunning']
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