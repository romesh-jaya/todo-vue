<template>
  <div class="card">{{ item }}</div>
</template>

<script>
export default {
  name: "Todo",
  props: { item: String },
};
</script>

<style scoped>
.card {
  display: grid;
  place-items: center;
  block-size: 2rem;
  inline-size: 20rem;
  margin: auto;
  border: 1px solid grey;
  background-color: antiquewhite;
  border-radius: 3px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  cursor: pointer;
}
</style>
