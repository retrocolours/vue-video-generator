<script lang="ts">
import { defineComponent } from "vue";
import TypeSelector from "./components/TypeSelector.vue";
import ActionSelector from "./components/ActionSelector.vue";
import VideoPlayer from "./components/VideoPlayer.vue";

type VideoTemplate = {
  id: string;
  name: string;
  actions: string[];
};

export default defineComponent({
  components: {
    TypeSelector,
    ActionSelector,
    VideoPlayer,
  },

  data() {
    return {
      videoTypes: [
        { id: "flowers", name: "Flowers", actions: ["water", "plant", "gift"] },
        { id: "fruits", name: "Fruits", actions: ["water", "plant", "gift"] },
      ] as VideoTemplate[],

      selectedTypeId: undefined as string | undefined,
      selectedAction: undefined as string | undefined,
      videoSrc: "",
    };
  },

  computed: {
    selectedType() {
      return this.videoTypes.find((t) => t.id === this.selectedTypeId) || null;
    },

    showMessage() {
      return !this.selectedTypeId || !this.selectedAction;
    },
  },

  methods: {
    updateType(typeId: string) {
      this.selectedTypeId = typeId;
      this.selectedAction = undefined; // Reset action when type changes
      this.updateVideoSrc(); // Update videoSrc when type changes
    },

    updateAction(action: string) {
      this.selectedAction = action;
      this.updateVideoSrc(); // Update videoSrc when action changes
    },

    updateVideoSrc() {
      if (!this.selectedTypeId || !this.selectedAction) {
        this.videoSrc = "";
      } else {
        this.videoSrc = `/videos/${this.selectedTypeId}-${this.selectedAction}.mp4`;
      }
    },
  },
});
</script>

<template>
  <div class="app-container">
    <header>
      <h1>Flowers & Fruits Video Generator</h1>
    </header>

    <main>
      <TypeSelector :types="videoTypes" :selected-id="selectedTypeId" @select-type="updateType" />
      <ActionSelector
        :actions="selectedType ? selectedType.actions : []"
        :selected-action="selectedAction"
        @select-action="updateAction"
      />
      <VideoPlayer :videoSrc="videoSrc" :showMessage="showMessage" />
    </main>

    <footer>
      <p>&copy; 2025 Flowers & Fruits Video Generator</p>
    </footer>
  </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  width: 100%;
  height: 100%;
}

.app-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  min-height: 100vh;
  background-color: lightgray;
}

header,
footer {
  width: 100vw;
  color: black;
  padding: 1rem;
  text-align: center;
  flex-shrink: 0;
  position: relative;
  background-color: paleturquoise;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

footer {
  margin-top: auto;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex-grow: 1;
  width: 100%;
  max-width: 800px;
  text-align: center;
  gap: 1rem;
  font-family: Georgia, "Times New Roman", Times, serif;
  font-size: 0.8rem;
  background-color: snow;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}
</style>
