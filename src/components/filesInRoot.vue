<template>
  <div class="root-files">
    <div v-for="(folder, i) in this.inRootFiles">
      <p class="root-files__item" @click="findIndex(i), sourceCreator(i, 'file')">
        {{ folder }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["inRootFiles"],
  emits: ["find", "srcCreate"],
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
.root-files {
  font-size: 2.2rem;
  padding: 5px 0;
}

.root-files__item {
  &:hover {
    color: red;
    cursor: pointer;
  }
}
</style>
