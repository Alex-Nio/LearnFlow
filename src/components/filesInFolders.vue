<template>
  <div
    class="subfolders"
    v-if="has_files && this.folderName === this.courseRootFiles[targetIndex]['Папка']"
  >
    <div v-if="this.inFolderFiles" class="sub-files">
      <p style="font-weight: bold; font-size: 2rem">Файлы</p>
      <p
        class="sub-folder-item"
        @click="sourceCreator(i, 'subfile')"
        v-for="(item, i) in this.inFolderFiles"
      >
        {{ item }}
      </p>
    </div>
    <div class="sub-folders">
      <p style="font-weight: bold; font-size: 2rem">Подпапки</p>
      <p
        class="sub-folder-item"
        @click="sourceCreator(i, 'subfolder', item), findSubFiles(i, item)"
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
