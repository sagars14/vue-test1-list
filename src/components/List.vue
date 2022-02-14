<template>
  <div>
    <table v-if="showTable" class="user-table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Created Date</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, i) in usersList" :key="i">
          <td>{{ user.name }}</td>
          <td>{{ formattedDate(user.created_at) }}</td>
        </tr>
      </tbody>
    </table>
    <p v-else>No User found with this name, please Add</p>
  </div>
</template>

<script>
import moment from 'moment';
export default {
  name: 'List',
  props: {
    usersList: {
      type: Array,
      required: true,
    },
    showTable: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {};
  },
  methods: {
    formattedDate(date) {
      return moment(date).fromNow();
    },
  },
};
</script>

<style lang="scss" scoped>
@use 'sass/list.scss';
</style>
