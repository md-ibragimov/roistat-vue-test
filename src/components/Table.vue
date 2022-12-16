<template>
  <div class="table">
    <div class="table-title">
      <h3 @click="$emit('sortUsers')" class="title-name">Имя</h3>
      <h3 class="title-phone">Телефон</h3>
    </div>
    <table-item-vue :widthStyle="50" :users="users" />
  </div>
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
  width: 100%;
  height: auto;
  overflow: auto;
  display: flex;
  flex-direction: column;
  .table-title {
    display: flex;
    .title-name {
      cursor: pointer;
    }
    .title-name,
    .title-phone {
      width: 50%;
      border: 1px solid;
      height: max-content;
      padding: 5px 10px;
    }
  }
}
</style>