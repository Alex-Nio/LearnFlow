<template>
  <div class="files" v-for="(folder, i) in this.contentFiles">
    <p @click="findIndex(i), sourceCreator(i, 'file')">
      {{ folder }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["contentFiles"],
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

<style lang="scss" scoped></style>
