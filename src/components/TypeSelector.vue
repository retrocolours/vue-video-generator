<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";

type VideoTemplate = {
  id: string;
  name: string;
  actions: string[];
};

export default defineComponent({
  props: {
    types: {
      type: Array as PropType<VideoTemplate[]>,
      required: true,
    },
    selectedId: {
      type: String,
      default: null,
    },
  },

  emits: ["select-type"],

  methods: {
    selectType(typeId: string) {
      this.$emit("select-type", typeId);
    },
  },
});
</script>

<template>
  <div class="type-selector">
    <h2>Select a Type:</h2>
    <div class="buttons">
      <button
        v-for="type in types"
        :key="type.id"
        :class="{ active: selectedId && type.id === selectedId }"
        @click="selectType(type.id)"
      >
        {{ type.name }}
      </button>
    </div>
  </div>
</template>

<style scoped>
.type-selector {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.buttons {
  display: flex;
  gap: 1rem;
}

button {
  padding: 10px 20px;
  border: none;
  background: #080808;
  color: white;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background: #959ca4;
}

button.active {
  background: paleturquoise;
  color: black;
}
</style>
