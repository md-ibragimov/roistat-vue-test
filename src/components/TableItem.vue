<template>
  <tr class="tr" v-if="!user.isChild && !user.children.length">
    <td class="td">{{ user.name }}</td>
    <td class="td">{{ user.phone }}</td>
  </tr>
  <template v-else-if="!user.isChild && user.children.length">
    <tr class="tr">
      <td class="td">+ {{ user.name }}</td>
      <td class="td">{{ user.phone }}</td>
    </tr>
    <tr :key="child.id" v-for="child in user.children">
      <td class="td-child">
        <div class="td-child-div">+ {{ child.name }}</div>
      </td>
      <td class="td">{{ child.phone }}</td>
    </tr>
  </template>
</template>

<script>
export default {
  methods: {},
  props: {
    user: {
      type: Object,
      required: true,
    },
    users: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.td {
  border: 1px solid;
  text-align: center;
}
.td-child {
  border: none !important;
}
.td-child-div {
  width: 90%;
  margin-left: auto;
  border-left: 1px solid;
  text-align: center;
  color: #fff;
  background-color: #000;
}
</style>