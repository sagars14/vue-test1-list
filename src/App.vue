<template>
  <div>
    <Table />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Table from './components/Table.vue';

export default defineComponent({
  name: 'App',
  components: { Table },
  setup() {
    // Setup
  },
});
</script>

<style lang="scss" module>
// Style
</style>
