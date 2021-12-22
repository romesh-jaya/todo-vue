<template>
  <div class="card" @click="onCardClicked">
    <p class="text">{{ item }}</p>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: { item: String, id: Number, editModeOn: Boolean },
  emits: ["todo-clicked"],
  methods: {
    onCardClicked() {
      this.$parent.$emit("todo-clicked", {
        id: this.id,
      });
    },
  },
};
</script>

<style scoped>
.card {
  display: grid;
  place-items: center;
  block-size: 2rem;
  margin: auto;
  padding-inline: 1rem;
  border: 1px solid grey;
  background-color: antiquewhite;
  border-radius: 3px;
}

.text {
  inline-size: 95%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  cursor: pointer;
}
</style>
