<template>
  <!-- Категории курсов -->
  <courses-categories :courses="courses" @open="openCategory"></courses-categories>
  <!-- Курсы -->
  <transition
    :duration="810"
    mode="out-in"
    enter-active-class="animate__animated animate__fadeInUp"
    leave-active-class="animate__animated animate__fadeOutDown"
  >
    <course-content
      v-if="this.activeCategoryIndex !== null"
      :category="activeCategory"
      :key="activeCategoryIndex"
    ></course-content>
  </transition>
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

<style lang="scss" scoped>
.course-list-enter-active,
.course-list-leave-active {
  transition: all 0.5s ease;
}
.course-list-enter-from,
.course-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

.course-list-move {
  transition: transform 0.4s ease;
}
</style>
