<template>
  <h2 class="header">My Todos</h2>
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
  padding: 0;
  margin: 0;
  font-family: "Roboto", sans-serif;
  height: 100%;
}

a {
  color: inherit;
  text-decoration: none;
}

* {
  box-sizing: border-box;
}

p {
  margin: 0;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-block-start: 60px;
  height: 100%;
  margin: 0;
  display: flex;
  flex-direction: column;
}

.header {
  padding-block: 60px;
  margin: 0;
}
</style>
