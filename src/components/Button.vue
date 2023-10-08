<script setup lang="ts">
// ----------------------------------------------------------------
// Props
// ----------------------------------------------------------------
interface Props {
  label: string
  onClick: () => void
}

const props = defineProps<Props>()
</script>

<template>
  <button
    :onclick="props.onClick"
    @keydown.enter="props.onClick"
    :label="props.label"
    class="button-comp"
  >
    {{ props.label }}
  </button>
</template>

<style>
.button-comp {
  padding: 0.5rem 1rem;
  background-color: white;
  border: 2px solid #5482c8;
  border-radius: 0.25rem;

  font-size: 16px;

  cursor: pointer;

  transition: all 150ms ease-in-out;
}

.button-comp:hover {
  box-shadow: 0 4px 8px rgba(28, 34, 36, 0.16);
}
</style>
