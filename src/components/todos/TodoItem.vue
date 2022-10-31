<!-- eslint-disable vue/no-mutating-props -->

<template>
  <div
    class="d-flex justify-content-between p-2 border-bottom"
  >
    <div class="d-flex align-items-center" :class="isCompleted ? 'line-through' : ''">
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
export default {
  data(props) {
    return {
      isCompleted: props.todo.isCompleted,
    };
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

<style>

.line-through {
  text-decoration: line-through;
}

</style>
