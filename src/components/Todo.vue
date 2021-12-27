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
    <Modal v-if="showDeleteModal" @modal-close="onModalClosed">
      <template v-slot:header>
        <h3>Delete Todo</h3>
      </template>
      <template v-slot:body>
        <p>Are you sure you wish to delete this Todo?</p>
      </template>
    </Modal>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Modal from "../common/Modal.vue";
import DeleteOutlined from "@ant-design/icons-vue/DeleteOutlined";

export default defineComponent({
  name: "Todo",
  props: { item: String, id: Number, editModeOn: Boolean },
  components: { DeleteOutlined, Modal },
  emits: ["todo-clicked", "todo-delete-clicked"],
  data() {
    return {
      showDeleteModal: false,
    };
  },
  methods: {
    onCardClicked() {
      this.$parent?.$emit("todo-clicked", {
        id: this.id,
      });
    },
    onDeleteClicked() {
      this.showDeleteModal = true;
    },
    onModalClosed(value: { retVal: boolean }) {
      const { retVal } = value;
      this.showDeleteModal = false;
      if (retVal) {
        this.$parent?.$emit("todo-delete-clicked", {
          id: this.id,
        });
      }
    },
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
