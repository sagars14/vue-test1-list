<template>
  <div class="main-container">
    <SearchBar
      :show-add-btn="showAddBtn"
      @add="addUser($event)"
      @find="findUser($event)" />
    <p v-show="showMatchFound" style="text-align: center; width: 710px">
      <span class="exact-match"><strong> Exact Match !</strong></span>
    </p>
    <div class="user-list">
      <div class="left-section">
        <List :users-list="users" :show-table="showTable" />
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
      showAddBtn: false,
      showTable: true,
      users: [],
      tempUsers: [],
    };
  },
  mounted() {
    const users = [
      {
        name: 'ashish',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'rahul',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'aanand',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'pushark',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'ravi',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'himanshu',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'deepak',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'ankit',
        created_at: moment(new Date().toString()),
      },
      {
        name: 'kuldeep',
        created_at: moment(new Date().toString()),
      },
    ];
    window.localStorage.setItem('users', JSON.stringify(users));
    window.localStorage.getItem('users');
    this.users = [...users];
  },
  methods: {
    findUser(uname) {
      if (this.users.length > 0) {
        const foundedUser = this.users?.find(
          (user) => user.name.toLowerCase() === uname.toLowerCase()
        );
        if (foundedUser && foundedUser !== undefined) {
          this.tempUsers = [...this.users];
          this.users = [foundedUser];
          this.showTable = true;
          this.showAddBtn = false;
          this.showMatchFound = true;
        } else {
          this.showMatchFound = false;
          this.showAddBtn = true;
          this.showTable = false;
        }
      }
      if (!uname && uname === '') {
        if (this.tempUsers.length > 0) this.users = [...this.tempUsers];
        this.showTable = true;
        this.showAddBtn = false;
      }
    },
    addUser(newUser) {
      console.log('new user', newUser);
      if (newUser && newUser !== '') {
        this.users.unshift({
          name: newUser,
          created_at: moment(new Date()),
        });
        this.showAddBtn = false;
        this.showTable = true;
        this.tempUsers = [...this.users];
        window.localStorage.removeItem('users');
        window.localStorage.setItem('users', JSON.stringify([...this.users]));
      }
    },
  },
});
</script>

<style lang="scss" scoped>
@use 'sass/table.scss';
</style>
