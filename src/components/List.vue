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
          <td>{{ user.created_at }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
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
};
</script>

<style lang="scss" scoped>
@use 'sass/list.scss';
</style>
