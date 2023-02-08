<template>
  <div
    class="subfolders"
    v-if="has_files && this.folderName === this.contentFolders[targetIndex]['Папка']"
  >
    <p
      class="sub-folder-item"
      @click="sourceCreator(i, 'subfolder')"
      v-for="(item, i) in this.SubFolders"
    >
      {{ item }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["has_files", "folderName", "contentFolders", "SubFolders", "targetIndex"],
  methods: {
    findIndex(i) {
      this.$emit("find", i);
    },
    sourceCreator(i, marker) {
      this.$emit("srcCreate", i, marker);
    },
  },
};
</script>

<style lang="scss" scoped>
.sub-folder-item {
  font-size: 2rem;

  &:hover {
    cursor: pointer;
    color: white;
  }
}
</style>
