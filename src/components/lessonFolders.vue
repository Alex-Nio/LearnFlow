<template>
  <div class="root-folders" v-for="(folder, i) in this.courseRootFiles">
    <div @click="findIndex(i), openFolder(i, folder)">
      <p class="root-folders__item">{{ folder["Папка"] }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["courseRootFiles"],
  emits: ["find", "open"],
  methods: {
    findIndex(i) {
      this.$emit("find", i);
    },
    openFolder(i, folder) {
      this.$emit("open", i, folder);
    },
  },
};
</script>

<style lang="scss" scoped>
.root-folders__item {
  font-size: 2.2rem;
  padding: 5px 0;

  &:hover {
    color: red;
    cursor: pointer;
  }
}
</style>
