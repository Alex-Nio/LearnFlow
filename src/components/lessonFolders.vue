<template>
  <div class="folder-content" v-for="(folder, i) in this.contentFolders">
    <p @click="findIndex(i), openFolder()" style="font-size: 2rem">
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

<style lang="scss" scoped></style>
