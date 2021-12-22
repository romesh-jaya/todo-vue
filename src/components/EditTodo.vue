<template>
  <div class="container">
    <div class="label">{{ todoToEdit ? "Edit Todo" : "Add Todo" }}</div>
    <textarea
      class="input"
      :value="input"
      @input="onChangeInput($event.target.value)"
    ></textarea>
    <p class="error">{{ error }}</p>
    <Button
      class="button-save"
      @on-click="onAddSaveButtonClick"
      :label="todoToEdit ? 'Edit' : 'Add'"
    >
    </Button>
    <Button
      class="button-cancel"
      @on-click="onCancelClick"
      v-if="todoToEdit"
      label="Cancel Edit"
    >
    </Button>
  </div>
</template>

<script>
import Button from "../common/Button.vue";

export default {
  name: "EditTodo",
  props: { todoToEdit: Object },
  components: { Button },
  data() {
    return {
      input: "",
      error: "",
    };
  },
  emits: ["on-add-save", "on-cancel-edit"],
  watch: {
    todoToEdit() {
      if (this.todoToEdit) {
        this.input = this.todoToEdit.item;
        this.error = "";
      }
    },
  },
  methods: {
    onChangeInput(value) {
      this.input = value;
      this.error = "";
    },
    resetForm() {
      this.error = "";
      this.input = "";
    },
    onAddSaveButtonClick() {
      if (!this.input) {
        this.error = "Todo cannot be empty";
        return;
      }

      this.$emit("on-add-save", {
        item: this.input,
        id: this.todoToEdit?.id,
      });

      this.resetForm();
    },
    onCancelClick() {
      this.$emit("on-cancel-edit", {
        id: this.todoToEdit?.id,
      });
      this.resetForm();
    },
  },
};
</script>

<style lang="scss" scoped>
.label {
  font-size: 1.175rem;
  margin-block-end: 0.5rem;
}

.input {
  block-size: 4rem;
  border: 1px solid grey;
  background-color: lavender;
  border-radius: 3px;
  inline-size: 100%;
  padding: 0.25rem;
  font-size: 1rem;
  font-family: inherit;
  margin-block-end: 0.5rem;
}

.button-cancel {
  margin-inline-start: 0.5rem;
  background-color: lavender;
}

.button-save {
  background-color: #5959ff;
  color: white;
}

.container {
  margin: auto;
  inline-size: 90%;
  max-inline-size: 300px;
}

.error {
  color: red;
  font-size: 0.75rem;
  margin-block-end: 0.5rem;
}
</style>
