<template>
  <div class="container">
    <div class="label">Add Todo</div>
    <textarea
      class="input"
      :value="input"
      @input="onChangeInput($event.target.value)"
    ></textarea>
    <p class="error">{{ error }}</p>
    <button class="button" @click="onAddSaveButtonClick">Add</button>
  </div>
</template>

<script>
export default {
  name: "EditTodo",
  props: { item: String },
  data() {
    return {
      input: "",
      error: "",
    };
  },
  emits: ["add-save-button-clicked"],
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

      this.$emit("add-save-button-clicked", { input: this.input, id: null });
      this.input = "";
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

.button {
  background-color: #5959ff;
  color: white;
  padding-inline: 0.5rem;
  padding-block: 0.25rem;
  border-radius: 3px;
  font-size: 1rem;
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
