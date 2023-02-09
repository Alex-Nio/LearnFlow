<template>
  <div class="root-folders" v-for="(folder, i) in this.courseRootFiles">
    <p class="root-folders__item" @click="findIndex(i), openFolder(i)">
      {{ folder["Папка"] }}
    </p>
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
    openFolder(i) {
      this.$emit("open", i);
    },
  },
};
</script>

<style lang="scss" scoped>
.root-folders__item {
  font-size: 2.2rem;

  &:hover {
    color: red;
    cursor: pointer;
  }
}
</style>
