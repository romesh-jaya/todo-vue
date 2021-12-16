<template>
  <h2>My Todos</h2>
  <TodoList />
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: { TodoList },
  data() {
    return {
      counter: 0,
      labelText: "Hello Rom",
    };
  },
  methods: {
    onButtonClick(newCount) {
      this.counter = newCount;
    },
    handler(e, data) {
      console.log("e", e);
      console.log("data", data);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto+Condensed");

html,
body {
  font-family: "Roboto", sans-serif;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
