<template>
  <button class="button" @click="$emit('on-click')">
    {{ label }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: { label: String },
  emits: ["on-click"],
};
</script>

<style>
.button {
  padding-inline: 0.5rem;
  padding-block: 0.25rem;
  border-radius: 3px;
  font-size: 1rem;
  border: 1px solid grey;
}
</style>
