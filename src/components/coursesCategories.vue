<template>
  <div class="courses-grid">
    <div class="courses" v-for="(category, index) in this.courses.categories">
      <div @click="openCategory(category, index)" class="course-title">
        {{ category[0] }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["courses"],
  emits: ["open"],
  methods: {
    openCategory(category, index) {
      this.$emit("open", category, index);
    },
  },
};
</script>

<style lang="scss" scoped>
.courses-grid {
  width: 100%;
  max-width: 1200px;
  display: grid;
  grid: repeat(3, 1fr) / repeat(1, 1fr);
  justify-items: center;
  margin: 0 auto 120px auto;
  overflow-y: scroll;
}
.course-title {
  font-size: 2.2rem;
  text-align: center;
  margin: 15px 0;
  cursor: pointer;

  &:hover {
    color: blue;
    transition: all 0.5s linear;
  }
}
</style>
