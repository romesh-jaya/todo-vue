<template>
  <div class="container">
    <div class="label">{{ label }}</div>
    <textarea
      class="input"
      :value="input"
      @input="onChangeInput($event.target.value)"
    ></textarea>
    <p class="error">{{ error }}</p>
    <button class="button-save" @click="onAddSaveButtonClick">
      {{ buttonName }}
    </button>
    <button class="button-cancel" @click="onCancelClick" v-if="todoToEdit">
      Cancel Edit
    </button>
  </div>
</template>

<script>
const labels = Object.freeze({ ADD: "Add Todo", EDIT: "Edit Todo" });
const buttonNames = Object.freeze({ ADD: "Add", EDIT: "Edit" });

export default {
  name: "EditTodo",
  props: { todoToEdit: Object },
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
      this.error = "";
      if (this.todoToEdit) {
        this.input = this.todoToEdit.item;
        this.label = labels.EDIT;
        this.buttonName = buttonNames.EDIT;
      } else {
        this.input = "";
        this.label = labels.ADD;
        this.buttonName = buttonNames.ADD;
      }
    },
  },
  methods: {
    onChangeInput(value) {
      this.input = value;
      this.error = "";
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
    },
    onCancelClick() {
      this.$emit("on-cancel-edit", {
        id: this.todoToEdit?.id,
      });
    },
  },
};
</script>

<style scoped>
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

.button-save {
  background-color: #5959ff;
  color: white;
  padding-inline: 0.5rem;
  padding-block: 0.25rem;
  border-radius: 3px;
  font-size: 1rem;
  border: 1px solid grey;
}

.button-cancel {
  margin-inline-start: 0.5rem;
  background-color: #5959ff28;
  padding-inline: 0.5rem;
  padding-block: 0.25rem;
  border-radius: 3px;
  font-size: 1rem;
  border: 1px solid grey;
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
