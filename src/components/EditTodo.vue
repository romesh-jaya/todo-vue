<template>
  <div class="container">
    <div class="label">{{ label }}</div>
    <textarea
      class="input"
      :value="input"
      @input="onChangeInput($event.target.value)"
    ></textarea>
    <p class="error">{{ error }}</p>
    <Button
      class="button-save"
      @on-click="onAddSaveButtonClick"
      :label="buttonName"
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

const labels = Object.freeze({ ADD: "Add Todo", EDIT: "Edit Todo" });
const buttonNames = Object.freeze({ ADD: "Add", SAVE: "Save" });

export default {
  name: "EditTodo",
  props: { todoToEdit: Object },
  components: { Button },
  data() {
    return {
      input: "",
      error: "",
      label: labels.ADD,
      buttonName: buttonNames.ADD,
    };
  },
  emits: ["on-add-save", "on-cancel-edit"],
  watch: {
    todoToEdit() {
      if (this.todoToEdit) {
        this.input = this.todoToEdit.item;
        this.label = labels.EDIT;
        this.buttonName = buttonNames.SAVE;
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
      this.label = labels.ADD;
      this.buttonName = buttonNames.ADD;
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

@media screen and (max-width: 2600px) {
  .error {
    color: blue;
  }
}
</style>
