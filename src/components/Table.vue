<template>
  <table class="table">
    <tr class="tr">
      <th
        style="cursor: pointer"
        @click="$emit('sortUsers')"
        scope="col"
        class="table-name"
      >
        Имя
      </th>
      <th scope="col" class="table-phone">Телефон</th>
    </tr>
    <TableItemVue
      :user="user"
      :users="users"
      :key="user.id"
      v-for="user in users"
    />
  </table>
</template>

<script>
import TableItemVue from "./TableItem.vue";

export default {
  components: { TableItemVue },
  props: {
    users: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.table {
  border: 1px solid;
  border-collapse: collapse;
}
.tr,
.table-name,
.table-phone {
  border: 1px solid;
}
</style>