<template>
  <div class="card" :class="{ 'card-edit': editModeOn }" @click="onCardClicked">
    <p class="text">{{ item }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Todo",
  props: { item: String, id: Number, editModeOn: Boolean },
  emits: ["todo-clicked"],
  methods: {
    onCardClicked() {
      this.$parent?.$emit("todo-clicked", {
        id: this.id,
      });
    },
  },
});
</script>

<style lang="scss" scoped>
@import "../styles/globals.scss";

.card {
  display: grid;
  place-items: center;
  block-size: 2rem;
  margin: auto;
  padding-inline: 1rem;
  border: 1px solid grey;
  background-color: $antique-white;
  border-radius: 3px;
}

.card-edit {
  background-color: $antique-white-highlight;
}

.text {
  inline-size: 95%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  cursor: pointer;
}
</style>
