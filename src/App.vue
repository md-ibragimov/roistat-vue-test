<template>
  <div class="container">
    <div class="table-container">
      <button @click="handleForm(true)" id="add-button" class="button">
        Добавить
      </button>
      <button
        @click="localStorageClean"
        id="local-storage-clean"
        class="button"
      >
        Очистить локальное хранилище
      </button>
      <TableVue @sortUsers="sortUsers" :users="users" />
    </div>
    <div class="form-container">
      <UserFormVue
        @addContact="addContact"
        @handleForm="handleForm"
        :form="form"
        :allUsers="allUsers"
        :users="users"
      />
    </div>
  </div>
</template>

<script>
import TableVue from "./components/Table.vue";
import UserFormVue from "./components/UserForm.vue";

export default {
  components: { TableVue, UserFormVue },
  data() {
    return {
      form: false,
      users: localStorage.getItem("users")
        ? JSON.parse(localStorage.getItem("users"))
        : [],
      allUsers: [],
    };
  },
  methods: {
    handleForm(value) {
      this.form = value;
    },
    addContact(value) {
      this.allUsers.push(value);
      if (!value.boss.id) {
        this.users.push({
          id: value.id,
          name: value.name,
          phone: value.phone,
          isChild: false,
          children: [],
        });
      } else {
        this.users = this.users.map((el) => {
          if (el.id === value.boss.id) {
            return {
              ...el,
              children: [
                ...el.children,
                {
                  name: value.name,
                  phone: value.phone,
                  id: value.id,
                  isChild: true,
                },
              ],
            };
          }
          return el;
        });
      }
    },
    localStorageClean() {
      this.users = [];
    },
    sortUsers() {
      this.users.map((el) => {
        return el.children.sort((a, b) =>
          a.name.toLowerCase() > b.name.toLowerCase() ? 1 : -1
        );
      });
      this.users.sort((a, b) =>
        a.name.toLowerCase() > b.name.toLowerCase() ? 1 : -1
      );
    },
  },
  watch: {
    users: {
      handler(value) {
        localStorage.setItem("users", JSON.stringify(value));
      },
      deep: true,
    },
  },
};
</script>

<style lang="scss">
.container {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: space-between;
  gap: 100px;
}

.button {
  padding: 5px 15px;
  border-radius: 1em;
  border: 0.5px solid;
  width: max-content;
  cursor: pointer;
}

.table-container {
  width: 50%;
  height: 100%;
  display: flex;
  flex-direction: column;
  overflow: auto;

  #add-button {
    flex-grow: 0;
    flex-shrink: 0;
    margin: 50px 0 35px auto;
  }
  #local-storage-clean {
    margin: 0 0 15px auto;
    flex-grow: 0;
    flex-shrink: 0;
  }
}

.form-container {
  width: 50%;
  height: 100%;
  overflow: auto;
}
</style>