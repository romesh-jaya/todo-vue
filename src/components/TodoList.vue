<template>
  <div class="container">
    <div v-for="todo in todos" :key="todo.id">
      <Todo :item="todo.item" />
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  name: "TodoList",
  components: { Todo },
  data() {
    return {
      todos: [
        { id: "111", item: "Go shopping" },
        { id: "112", item: "Bake cake" },
        { id: "113", item: "Wash dog" },
      ],
    };
  },
};
</script>

<style scoped>
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  row-gap: 1.5rem;
  max-inline-size: 900px;
  inline-size: 90%;
  margin: auto;
}
</style>
