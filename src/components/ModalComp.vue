<template>
  <div class="backdrop d-flex align-items-center justify-content-center">
    <div class="bg-light text-center p-4 rounded">
      <h2 class="text-dark">Edit Todo</h2>
      <div class="d-flex my-4">
        <input class="mx-3" type="text" v-model="title" />
        <input type="checkbox" v-model="completed" />
      </div>
      <div>
        <button class="btn btn-danger" @click="closeModal">Cancel</button>
        <button class="btn btn-success" @click="updateTodo">Edit Todo</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(props) {
    return {
      title: props.todo.title,
      completed: props.todo.isCompleted,
    };
  },
  props: {
    todo: Object,
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    updateTodo() {
      const todo = {
        id: this.todo.id,
        title: this.title,
        isCompleted: this.completed,
      };
      this.$emit("update", todo);
    },
  },
};
</script>

<style>
.backdrop {
  position: absolute;
  top: 0;
  width: 100%;
  height: 100vh;
  background-color: rgb(0, 0, 0, 0.5);
}
</style>
