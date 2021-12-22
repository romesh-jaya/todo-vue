<template>
  <div class="container">
    <div v-for="todo in todos" :key="todo.id">
      <Todo :item="todo.item" :id="todo.id" :edit-mode-on="todo.editModeOn" />
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  name: "TodoList",
  components: { Todo },
  props: { todos: Array },
};
</script>

<style scoped>
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  row-gap: 1.5rem;
  max-inline-size: 300px;
  inline-size: 90%;
  margin: auto;
}
</style>
