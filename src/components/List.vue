<template>
  <div>
    <table class="user-table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Created Date</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, i) in usersList" :key="i">
          <td>{{ user.name }}</td>
          <td>{{ formattedDate(user.created_at) }}</td>
        </tr>
      </tbody>
    </table>
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
