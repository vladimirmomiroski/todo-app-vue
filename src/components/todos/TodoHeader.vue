<template>
  <form
    @submit.prevent="onSubmitHandler"
    class="col-10 col-md-8 py-4 px-3 d-flex justify-content-between bg-light rounded"
  >
    <input
      class="px-2 bg-light rounded"
      type="text"
      v-model="todoTitle"
      placeholder="Todo..."
    />
    <button class="btn btn-info btn-dark">Add Todo</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      todoTitle: "",
    };
  },

  methods: {
    onSubmitHandler() {
      if (this.todoTitle.trim()) {
        const id = new Date().valueOf();
        const todo = {
          id,
          title: this.todoTitle,
          isCompleted: false,
        };
        this.addTodo(todo);
        this.todoTitle = ""
      }
    },
    addTodo(todo) {
      const options = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(todo)
      };
      fetch("http://localhost:3000/todos", options)
      .then(res => {
        if(res.status === 201) {
            this.$emit('refetch')
        }
      })
      .catch(error =>  {
        throw new Error(error)
    })
    },
  },
};
</script>
