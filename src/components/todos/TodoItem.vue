
<template>
  <div
    class="d-flex justify-content-between p-2 border-bottom"
  >
    <div class="d-flex align-items-center">
      <p class="m-0">{{ todo.title }}</p>
      <input @click="toggleTodo(todo, todo.isCompleted)" class="mx-2" type="checkbox" v-model="todo.isCompleted" />
    </div>
    <div>
      <button @click="openModal(todo)" class="btn btn-outline-warning mx-2">
        Edit
      </button>
      <button class="btn btn-danger" @click="deleteTodo(todo.id)">
        Delete
      </button>
    </div>
  </div>
</template>

<script>
import ModalComp from "../ModalComp.vue";
export default {
  data(props) {
    return {
      isCompleted: props.todo.isCompleted,
    };
  },
  components: {
    ModalComp,
  },
  props: {
    todo: Object,
  },
  methods: {
    deleteTodo(id) {
      this.$emit("delete", id);
    },
    toggleTodo(item, isCompleted) {
      this.$emit("toggle", item, isCompleted);
    },
    openModal(todo) {
    this.$emit('open', todo)
  }
  },

};
</script>

<style></style>
