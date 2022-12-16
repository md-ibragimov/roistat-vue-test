<template>
  <div v-if="form" class="user-form-container">
    <div @click="$emit('handleForm', false)" class="use-form-close">x</div>
    <h3 class="user-form-title">Добавление пользователя</h3>
    <form @submit.prevent @submit="handleForm" class="user-form">
      <label class="user-form-label"
        >Имя<input
          required
          v-model="contact.name"
          class="user-form-item"
          type="text"
      /></label>
      <label class="user-form-label"
        >Телефон<input
          required
          v-model="contact.phone"
          class="user-form-item"
          type="tel"
      /></label>
      <label class="user-form-label">
        Начальник
        <select
          :value="contact.boss.id"
          @input="handleSelect"
          class="user-form-item"
        >
          <option v-for="user in allUsers" :value="user.id" :key="user.id">
            {{ user.name }}
          </option>
        </select>
      </label>
      <input type="submit" id="save-button" class="button" value="Сохранить" />
    </form>
  </div>
</template>

<script lang="js">
import { v4 } from "uuid";

export default {
  data() {
    return {
      contact: {
        id: v4(),
        name: null,
        phone: null,
        boss: {
          id: null,
          name: null,
          phone: null,
        },
      },
    };
  },
  methods: {
    handleSelect(event) {
      this.contact.boss.id = event.target.value;
      this.allUsers.map((el) => {
        if (el.id && event.target.value) {
          this.contact.boss.name = el.name;
          this.contact.boss.phone = el.phone;
        }
      })[0];
    },
    handleForm() {
      this.$emit("addContact", this.contact);
      this.contact = {
        id: v4(),
        name: null,
        phone: null,
        boss: {
          id: null,
          name: null,
          phone: null,
        },
      };
    },
  },
  watch: {
    form: {
      handler(value) {
        if (!value) {
          this.contact = {
            id: v4(),
            name: null,
            phone: null,
            boss: {
              id: null,
              name: null,
              phone: null,
            },
          };
        }
      },
      deep: true,
    },
  },
  props: {
    allUsers: {
      type: Array,
      required: true,
    },
    users: {
      type: Array,
      required: true,
    },
    form: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.user-form-container {
  width: 100%;
  height: max-content;
  margin: 100px auto 0 auto;
  border: 2px solid;
  display: flex;
  flex-direction: column;
  padding: 10px 15px;
  align-items: center;
  position: relative;

  margin-right: auto;
  flex-grow: 0;
  flex-shrink: 0;

  .use-form-close {
    position: absolute;
    top: 0;
    right: 10px;
    cursor: pointer;
    font-weight: 600;
    font-size: 22px;
  }

  .user-form {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 40px 0;
    align-items: center;

    .user-form-label {
      width: 100%;
      display: flex;
      justify-content: space-between;
    }

    .user-form-item {
      width: 100%;
      margin-left: 15px;
    }
  }
}
</style>