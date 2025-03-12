<script lang="ts">
import { defineComponent, ref, watch } from "vue";

export default defineComponent({
  props: {
    videoSrc: {
      type: String,
      required: true,
    },
    showMessage: {
      type: Boolean,
      required: true,
    },
  },

  setup(props) {
    const videoKey = ref(props.videoSrc);

    // Watch for changes in videoSrc and force video element reset
    watch(
      () => props.videoSrc,
      (newSrc) => {
        videoKey.value = "";
        setTimeout(() => {
          videoKey.value = newSrc;
        }, 10); // Small delay to allow DOM reset
      }
    );

    return { videoKey };
  },
});
</script>

<template>
  <div class="video-player">
    <h2>Generated Video:</h2>
    <p v-if="showMessage">Please select an action and a type to generate a video.</p>
    <video v-else controls :key="videoKey">
      <source :src="videoKey" type="video/mp4" />
      Your browser does not support the video tag.
    </video>
  </div>
</template>

<style scoped>
.video-player {
  width: 100%;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 1rem;
}

video {
  width: 100%;
  max-width: 100%;
  border-radius: 10px;
}
</style>
