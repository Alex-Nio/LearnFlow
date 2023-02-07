<template>
  <!-- Категории курсов -->
  <courses-categories :courses="courses" @open="openCategory"></courses-categories>
  <!-- Курсы -->
  <course-content
    v-if="this.activeCategoryIndex !== null"
    :category="activeCategory"
  ></course-content>
</template>

<script>
import coursesCategories from "./coursesCategories.vue";
import courseContent from "./courseContent.vue";
export default {
  props: {
    courses: {
      type: Object,
      required: true,
    },
  },
  components: {
    coursesCategories,
    courseContent,
  },
  data() {
    return {
      showCategory: false,
      activeCategory: "",
      activeCategoryIndex: null,
      trigger: false,
    };
  },
  methods: {
    openCategory(category, index) {
      this.activeCategoryIndex = index;
      this.activeCategory = category;
      this.trigger = true;
    },
  },
};
</script>

<style lang="scss" scoped></style>
