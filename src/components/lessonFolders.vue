<template>
  <div class="folder-content" v-for="(folder, i) in this.contentFolders">
    <p class="folder-content__item" @click="findIndex(i), openFolder()">
      {{ folder["Папка"] }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["contentFolders"],
  emits: ["find", "open"],
  methods: {
    findIndex(i) {
      this.$emit("find", i);
    },
    openFolder() {
      this.$emit("open");
    },
  },
};
</script>

<style lang="scss" scoped>
.folder-content__item {
  font-size: 2.2rem;

  &:hover {
    color: red;
    cursor: pointer;
  }
}
</style>
