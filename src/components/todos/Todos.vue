<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="pt-5 row mx-auto justify-content-center">
    <TodoHeader @refetch="getDataHandler(url)" />
    <TodoBody
      :todos="todos"
      @delete="deleteTodoHandler"
      @toggle="toggleTodoHandler"
      @open="openModal"
    />
    <Teleport to="#modals">
      <ModalComp v-if="modalActive" @close="closeModal" @update="updateTodoHandler" :todo="todoToUpdate" />
    </Teleport>
  </div>
</template>

<script>
import TodoBody from "./TodoBody.vue";
import TodoHeader from "./TodoHeader.vue";
import ModalComp from "../ModalComp.vue";
export default {
  components: {
    TodoHeader,
    TodoBody,
    ModalComp,
  },
  data() {
    return {
      todos: [],
      url: "http://localhost:3000/todos",
      modalActive: false,
      todoToUpdate: null
    };
  },
  mounted() {
    this.getDataHandler(this.url);
  },
  methods: {
    getDataHandler(url) {
      fetch(url)
        .then(res => res.json())
        .then(data => {
          this.todos = data
          console.log(this.todos)
        });
    },
    deleteTodoHandler(id) {
      const options = {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
        },
      };

      fetch("http://localhost:3000/todos/" + id, options)
        .then((res) => {
          if (res.status === 200) {
            this.getDataHandler(this.url);
          }
        })
        .catch((error) => {
          console.log(error, "error");
          throw new Error(error);
        });
    },
    toggleTodoHandler(item, isCompleted) {
      console.log("zasho se aktivira ova");
      const options = {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ ...item, isCompleted: !isCompleted }),
      };

      fetch("http://localhost:3000/todos/" + item.id, options)
        .then((res) => {
          if (res.status === 200) {
            this.getDataHandler(this.url);
          }
        })
        .catch((error) => {
          console.log(error, "error");
          throw new Error(error);
        });
    },
    openModal(todo) {
      this.todoToUpdate = todo
      this.modalActive = true
    },
    closeModal() {
      this.modalActive = false
    },
    updateTodoHandler(todo) {
      const options = {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(todo),
      };

      fetch("http://localhost:3000/todos/" + todo.id, options)
        .then((res) => {
          if (res.status === 200) {
            this.closeModal()
            this.getDataHandler(this.url);
          }
        })
        .catch((error) => {
          console.log(error, "error");
          throw new Error(error);
        });
    }
  },
};
</script>

<style></style>
