<template>
  <div class="container">
    <div class="label">Add Todo</div>
    <textarea class="input"></textarea>
  </div>
</template>

<script>
export default {
  name: "EditTodo",
  props: { item: String },
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
}

.container {
  margin: auto;
  inline-size: 90%;
  max-inline-size: 300px;
}
</style>
