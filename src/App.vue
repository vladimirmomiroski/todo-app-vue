<template>
    <Navbar />
    <Todos />
</template>

<script>
import Navbar from "./components/Navbar";
import Todos from "./components/todos/Todos";
import "./assets/GlobalStyles.css";

export default {
  name: "App",

  components: {
    Navbar,
    Todos,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

</style>
