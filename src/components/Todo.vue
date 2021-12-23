<template>
  <div class="container-card">
    <div
      class="card"
      :class="{ 'card-edit': editModeOn }"
      @click="onCardClicked"
    >
      <p class="text">{{ item }}</p>
    </div>
    <div class="icon" @click="onDeleteClicked">
      <DeleteOutlined />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import DeleteOutlined from "@ant-design/icons-vue/DeleteOutlined";

export default defineComponent({
  name: "Todo",
  props: { item: String, id: Number, editModeOn: Boolean },
  components: { DeleteOutlined },
  emits: ["todo-clicked", "todo-delete-clicked"],
  methods: {
    onCardClicked() {
      this.$parent?.$emit("todo-clicked", {
        id: this.id,
      });
    },
    onDeleteClicked() {},
  },
});
</script>

<style lang="scss" scoped>
@import "../styles/globals.scss";

.container-card {
  display: flex;
  flex-wrap: nowrap;
}

.card {
  display: grid;
  place-items: center;
  block-size: 2rem;
  margin: auto;
  padding-inline: 1rem;
  border: 1px solid grey;
  background-color: $antique-white;
  border-radius: 3px;
  inline-size: 100%;
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

.icon {
  block-size: 2rem;
  margin-inline-start: 1rem;
  display: flex;
  place-items: center;
  cursor: pointer;
}
</style>
