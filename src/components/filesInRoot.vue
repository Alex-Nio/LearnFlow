<template>
  <div class="files">
    <div v-for="(folder, i) in this.inRootFiles">
      <p @click="findIndex(i), sourceCreator(i, 'file')">
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
.files {
  margin-top: 10px;
  font-size: 2.2rem;
}
</style>
