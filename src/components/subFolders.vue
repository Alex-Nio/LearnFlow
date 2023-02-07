<template>
  <div
    class="subfolders"
    v-if="has_files && this.folderName === this.contentFolders[targetIndex]['Папка']"
  >
    <p @click="defaultOpen(i, 'folder')" v-for="(item, i) in this.SubFolders">
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
    defaultOpen(i, marker) {
      this.$emit("default", i, marker);
    },
  },
};
</script>

<style lang="scss" scoped></style>
