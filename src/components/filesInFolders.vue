<template>
  <div class="subfolders" v-if="has_files">
    <button @click="closePanel" class="video-close-btn">
      <img src="../assets/img/video-close-white.svg" alt="" />
    </button>
    <div v-if="this.inFolderFiles" class="sub-files">
      <p
        class="sub-folder-item"
        @click="sourceCreator(i, 'subfile'), openVideo()"
        v-for="(item, i) in this.inFolderFiles"
      >
        {{ item }}
      </p>
    </div>
    <div class="sub-folders">
      <p
        class="sub-folder-item"
        @click="sourceCreator(i, 'subfolder', item), findSubFiles(i, item), openVideo()"
        v-for="(item, i) in this.inFolderFolders"
      >
        {{ item }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    "has_files",
    "folderName",
    "courseRootFiles",
    "inFolderFiles",
    "inFolderFolders",
    "targetIndex",
  ],
  methods: {
    sourceCreator(i, marker, item) {
      this.$emit("srcCreate", i, marker, item);
    },
    findSubFiles(i, item) {
      this.$emit("findSubFiles", i, item);
    },
    openVideo() {
      this.$emit("openVideo");
    },
    closePanel() {
      this.$emit("closePanel");
    },
  },
};
</script>

<style lang="scss" scoped>
.subfolders {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translate(-50%, 0);
  width: calc(100% - 40px);
  height: 100%;
  min-height: calc(100vh - 40px - 75px);
  padding: 35px;
  /* From https://css.glass */
  background: rgba(82, 183, 136, 0.42);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(9.6px);
  -webkit-backdrop-filter: blur(9.6px);
  border: 1px solid rgba(82, 183, 136, 0.09);
  overflow: hidden;
  overflow-y: scroll;
  animation: fadeIn 0.5s linear;
}
.sub-folder-item {
  font-size: 1.8rem;
  margin: 5px 0;

  &:hover {
    cursor: pointer;
    color: #d8f3dc;
  }
}
</style>
