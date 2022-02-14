<template>
  <div class="search-bar">
    <input
      v-model="searchValue"
      placeholder="Search or Add..."
      type="search"
      @keyup.enter="$emit('add', searchValue)" />
    <button
      v-show="showAddBtn"
      type="submit"
      @click="$emit('add', searchValue)">
      <strong>Add</strong>
    </button>
  </div>
</template>

<script>
import { defineComponent } from '@vue/runtime-core';

export default defineComponent({
  name: 'SearchBar',
  props: {
    showAddBtn: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      searchValue: '',
    };
  },
  watch: {
    searchValue() {
      this.$emit('find', this.searchValue);
    },
  },
});
</script>

<style lang="scss" scoped>
@use 'sass/searchBar.scss';
</style>
