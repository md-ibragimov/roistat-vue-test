<template>
  <template :key="user.id" v-for="user in users">
    <div class="contact-wrapper" v-if="!user.children.length">
      <div :style="{ width: `${widthStyle}%` }" class="user-name">
        {{ children ? `+ ${user.name}` : user.name }}
      </div>
      <div v-if="!user.children.length" class="user-phone">
        {{ user.phone }}
      </div>
    </div>
    <template v-else>
      <div class="contact-wrapper">
        <div :style="{ width: `${widthStyle}%` }" class="user-name">
          + {{ user.name }}
        </div>
        <div class="user-phone">
          {{ user.phone }}
        </div>
      </div>
      <TableItem
        :widthStyle="widthStyle - 2"
        :children="true"
        :users="user.children"
      />
    </template>
  </template>
</template>

<script>
export default {
  name: "TableItem",
  props: {
    users: {
      type: Array,
      required: true,
    },
    children: {
      type: Boolean,
      required: false,
    },
    widthStyle: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.contact-wrapper {
  width: 100%;
  display: flex;
  margin-left: auto;
  .user-name,
  .user-phone {
    display: block;
    height: auto;
    border: 1px solid;
    padding: 5px 10px;
    width: 50%;
  }
  .user-name {
    margin-left: auto;
    align-items: flex-end;
  }
  .user-name-children {
    width: 45%;
  }
}
</style>