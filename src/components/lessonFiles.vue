<template>
  <div class="files" v-for="(folder, i) in this.contentFiles">
    <p @click="findIndex(i), defaultOpen(i, 'file')" style="font-size: 2rem">
      {{ folder }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["contentFiles"],
  emits: ["find", "default"],
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
