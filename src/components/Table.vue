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
        <List
          :users-list="users"
          :show-table="showTable"
          @delete="deleteUser($event)" />
      </div>
      <div class="right-section">
        <div style="margin-top: 1em">
          <div class="sort-by" style="margin-bottom: 2em">
            <input id="name" v-model="picked" type="radio" value="name" />
            <label for="name"
              ><span style="color: #a3a9af">Sort by</span> Value:
              <span v-if="picked === 'name'" class="sort-by-value"></span>
            </label>
          </div>
          <div class="sort-by">
            <input id="date" v-model="picked" type="radio" value="date" />
            <label for="date"
              ><span style="color: #a3a9af">Sort by</span> Added Date:
              <span v-if="picked === 'date'" class="sort-by-date"></span
            ></label>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import List from './List.vue';
import SearchBar from './SearchBar.vue';
import moment from 'moment';

interface User {
  name: string;
  created_at: string | Date | any;
}
export default defineComponent({
  name: 'Table',
  components: { List, SearchBar },
  data(): any {
    return {
      showAddBtn: false,
      showTable: true,
      users: [],
      tempUsers: [],
      picked: '',
    };
  },
  watch: {
    picked(pickedValue: string): void {
      console.log(pickedValue);
      if (pickedValue === 'name') {
        this.users.sort((a: User, b: User): number => {
          var nameA = a.name.toUpperCase(); // ignore upper and lowercase
          var nameB = b.name.toUpperCase(); // ignore upper and lowercase
          if (nameA < nameB) {
            return -1;
          }
          if (nameA > nameB) {
            return 1;
          }

          // names must be equal
          return 0;
        });
      } else {
        console.log('sort by date');
        this.users.sort((a: User, b: User) => {
          return b.created_at - a.created_at;
        });
      }
    },
  },
  mounted() {
    const users = [
      {
        name: 'ashish',
        created_at: moment(new Date().toString()).day(-1),
      },
      {
        name: 'rahul',
        created_at: moment(new Date().toString()).day(-2),
      },
      {
        name: 'aanand',
        created_at: moment(new Date().toString()).day(-3),
      },
      {
        name: 'pushark',
        created_at: moment(new Date().toString()).day(-4),
      },
      {
        name: 'ravi',
        created_at: moment(new Date().toString()).day(-5),
      },
      {
        name: 'himanshu',
        created_at: moment(new Date().toString()).day(-6),
      },
      {
        name: 'deepak',
        created_at: moment(new Date().toString()).day(-7),
      },
      {
        name: 'ankit',
        created_at: moment(new Date().toString()).day(0),
      },
      {
        name: 'kuldeep',
        created_at: moment(new Date().toString()),
      },
    ];
    window.localStorage.setItem('users', JSON.stringify(users));
    window.localStorage.getItem('users');
    this.users = [...users];
    this.picked = 'name';
  },
  methods: {
    findUser(uname: string): void {
      if (this.users.length > 0) {
        const foundedUser = this.users?.find(
          (user: User) => user.name.toLowerCase() === uname.toLowerCase()
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
        console.log('uname');
        if (this.tempUsers.length > 0) this.users = [...this.tempUsers];
        this.showTable = true;
        this.showAddBtn = false;
      }
    },
    addUser(newUser: string): void {
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
    deleteUser(name: string) {
      const newUsers = this.users.filter(
        (user: User) => user.name.toLowerCase() !== name.toLowerCase()
      );
      this.users = [...newUsers];
      this.tempUsers = [...newUsers];
      window.localStorage.removeItem('users');
      window.localStorage.setItem('users', JSON.stringify([...newUsers]));
    },
  },
});
</script>

<style lang="scss" scoped>
@use 'sass/table.scss';
</style>
