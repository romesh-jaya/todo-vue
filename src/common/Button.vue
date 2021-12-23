<template>
  <button
    class="button"
    :class="{ disabled: disabled }"
    @click="$emit('on-click')"
    :disabled="disabled"
  >
    {{ label }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: { label: String, disabled: Boolean },
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
  cursor: pointer;
}

.disabled {
  background-color: grey !important;
  cursor: inherit !important;
}
</style>
