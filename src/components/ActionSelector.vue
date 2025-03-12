<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    actions: {
      type: Array as () => string[],
      required: true,
    },
    selectedAction: {
      type: String,
      default: null,
    },
  },

  emits: ["select-action"],

  methods: {
    selectAction(event: Event) {
      const selectedValue = (event.target as HTMLSelectElement).value;
      this.$emit("select-action", selectedValue || null);
    },
  },
});
</script>

<template>
  <div class="action-selector">
    <h2>Select an Action:</h2>
    <select @change="selectAction" :value="selectedAction || ''">
      <option value="" disabled>Select an action...</option>
      <option v-for="action in actions" :key="action" :value="action">
        {{ action.charAt(0).toUpperCase() + action.slice(1) }}
      </option>
    </select>
  </div>
</template>

<style scoped>
.action-selector {
  display: flex;
  gap: 1rem;
}
</style>
