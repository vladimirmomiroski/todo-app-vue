<template>
  <ul class="col-10 col-md-8">
    <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" @delete="deleteTodoHandler" @toggle="toggleTodoHandler" @open="openModal" />
  </ul>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  props: {
    todos: Array,
  },
  components: {
    TodoItem,
  },
  methods: {
    deleteTodoHandler(id) {
        this.$emit('delete', id)
    },
    toggleTodoHandler(item, isCompleted) {
        this.$emit('toggle', item, isCompleted)
    },
    openModal(todo) {
      this.$emit('open', todo)
    }
  }
};
</script>

<style></style>
