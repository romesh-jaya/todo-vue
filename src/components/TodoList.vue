<template>
  <div class="container">
    <div v-for="todo in todos" :key="todo.id">
      <Todo :item="todo.item" :id="todo.id" :edit-mode-on="todo.editModeOn" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { Todo as TodoType } from "../types/Todo";
import Todo from "./Todo.vue";

export default defineComponent({
  name: "TodoList",
  components: { Todo },
  props: { todos: Array as PropType<Array<TodoType>> },
});
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
