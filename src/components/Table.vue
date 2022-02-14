<template>
  <div class="main-container">
    <SearchBar />
    <div class="user-list">
      <div class="left-section">
        <List :users-list="users" />
      </div>
      <div class="right-section"></div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import List from './List.vue';
import SearchBar from './SearchBar.vue';
import moment from 'moment';

export default defineComponent({
  name: 'Table',
  components: { List, SearchBar },
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    const users = [
      {
        name: 'ashish',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'rahul',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'aanand',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'pushark',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'ravi',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'himanshu',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'deepak',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'ankit',
        created_at: moment(new Date()).fromNow(),
      },
      {
        name: 'kuldeep',
        created_at: moment(new Date()).fromNow(),
      },
    ];
    window.localStorage.setItem('users', JSON.stringify(users));
    window.localStorage.getItem('users');
    this.users = [...users];
  },
});
</script>

<style lang="scss" scoped>
@use 'sass/table.scss';
</style>
