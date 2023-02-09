<template>
  <div class="video">
    <button @click="closeVideo" class="video-close-btn">
      <img src="../assets/img/video-close-white.svg" alt="" />
    </button>
    <div id="video" class="test-player-wrap">
      <vue3-video-player
        :src="source"
        :title="fileName"
        @ended="playEnded"
        cover="https://i.ytimg.com/vi/poPoWF3wSYI/maxresdefault.jpg"
      >
      </vue3-video-player>
    </div>
  </div>
</template>

<script>
export default {
  props: ["source", "fileName"],
  methods: {
    playEnded(e) {
      console.log(e);
      if (e.target === document.pictureInPictureElement) {
        document.exitPictureInPicture();
      }
    },
    closeVideo() {
      this.$emit("closeVideo");
    },
  },
};
</script>

<style lang="scss">
.video {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  max-width: 1200px;
  // background-image: linear-gradient(-225deg, #ffe29f 0%, #ffa99f 48%, #ff719a 100%);
  border-radius: 1rem;
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
  z-index: 50;
}

.video-close-btn {
  position: absolute;
  top: 30px;
  right: 30px;
  width: 45px;
  height: 45px;
  background: transparent;
  cursor: pointer;
  z-index: 25;

  & img {
    display: block;
    width: 100%;
    height: 100%;
  }
}

.test-player-wrap {
  width: 100%;
  height: 100%;
  position: relative;
  margin: 15px auto;
  animation: fadeIn 0.5s ease-in-out;
}

.btn-play {
  color: white;
  margin-right: 10px;
  cursor: pointer;
}

.btn-play svg {
  width: 16px;
}

.vcp-dashboard {
  width: 100% !important;
  margin: 0 !important;
}

.cover-layer,
.vcp-layer,
.error-layer,
.title-layer,
.video,
.loading-layer,
.play-pause-layer,
.cover-layer img,
.error-layer .error-msg-wrap,
.title-layer,
.title-layer .video-title,
.vcp-dashboard,
.vue-core-video-player-layers,
.vcp-container,
.vcp-container video {
  border-radius: 1rem !important;
}
</style>
