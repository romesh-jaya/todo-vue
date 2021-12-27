<template>
  <h2 class="header">My Todos</h2>
  <div class="content">
    <EditTodo
      @on-add-save="onAddSaveButtonClick"
      @on-cancel-edit="onCancelledEdit"
      :todo-to-edit="toDoInEditMode"
    />
    <TodoList
      :todos="todos"
      @todo-clicked="onTodoClicked"
      @todo-delete-clicked="onTodoDeleteClicked"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Todo } from "./types/Todo";
import TodoList from "./components/TodoList.vue";
import EditTodo from "./components/EditTodo.vue";

export default defineComponent({
  name: "App",
  components: { TodoList, EditTodo },
  data() {
    return {
      todos: [
        { id: 111, item: "Go shopping", editModeOn: false },
        { id: 112, item: "Bake cake", editModeOn: false },
        {
          id: 113,
          item: "Wash dog in the outside bathroom without soap",
          editModeOn: false,
        },
      ] as Todo[],
      toDoInEditMode: undefined as Todo | undefined,
    };
  },
  watch: {
    todos() {
      this.toDoInEditMode = this.todos.find((todo) => todo.editModeOn);
    },
  },
  methods: {
    onAddSaveButtonClick(value: Todo) {
      const { id, item } = value;

      if (id) {
        // Save edit to todo being edited
        const newArray = this.todos.map((todo) => {
          if (todo.id === id) {
            return {
              id,
              item,
              editModeOn: false,
            };
          }
          return todo;
        });
        this.todos = newArray;
      } else {
        // insert new todo
        const maxId = Math.max(...this.todos.map((todo) => todo.id));
        this.todos.push({
          id: maxId + 1,
          item,
          editModeOn: false,
        });
      }
    },
    onCancelledEdit(value: Todo) {
      const { id } = value;

      if (id) {
        const newArray = this.todos.map((todo) => {
          if (todo.id === id) {
            return {
              ...todo,
              editModeOn: false,
            };
          }
          return todo;
        });
        this.todos = newArray;
      }
    },
    onTodoDeleteClicked(value: Todo) {
      const { id } = value;

      if (id) {
        const newArray = this.todos.filter((todo) => todo.id !== id);
        this.todos = newArray;
      }
    },
    onTodoClicked(value: Todo) {
      const { id } = value;
      if (id) {
        const newArray = this.todos.map((todo) => {
          if (todo.id === id) {
            return {
              ...todo,
              editModeOn: true,
            };
          }
          return {
            ...todo,
            editModeOn: false,
          };
        });
        this.todos = newArray;
      }
    },
  },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto+Condensed");

html,
body {
  padding: 0;
  margin: 0;
  font-family: "Roboto", sans-serif;
  height: 100%;
  color: #2c3e50;
  font-size: 1rem;
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

.content {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1.5rem;
  max-inline-size: 1200px;
  inline-size: 90%;
  margin-inline: auto;
}
</style>
