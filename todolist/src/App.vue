<template>
  <todolist></todolist>
</template>

<script>
import todolist from "./components/todolist.vue";

export default {
  name: "App",
  components: {
    todolist,
  },
};
</script>
<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
nav {
  margin-top: 20px;
}
nav a {
  font-weight: bold;
  padding: 30px;
  box-sizing: border-box;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
