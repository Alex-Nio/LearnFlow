<template>
  <div class="full-wrapper">
    <header class="header">
      <nav class="nav">
        <router-link class="nav-item" to="/">На Главную</router-link>
      </nav>
    </header>
    <div class="container">
      <router-view :courses="courses" :pageName="this.$route.params.pageName" />
    </div>
  </div>
</template>

<script>
import coursesData from "@/assets/data/courses";

export default {
  data() {
    return {
      courses: {
        categories: [],
      },
    };
  },
  mounted() {
    const data = JSON.parse(JSON.stringify(coursesData));
    const courses = data["Курсы"];
    let coursesCategoryList = [];

    courses.forEach((course) => {
      let x = Object.entries(course);
      coursesCategoryList.push(x[0]);
    });

    this.courses.categories = coursesCategoryList;
  },
};
</script>

<style lang="scss">
@import "./assets/scss/imports.scss";

.header {
  width: 100%;
  height: 100px;
}
.nav {
  @include fdrjs_aic;
  width: 100%;
  height: 100%;
  padding: 0 45px;
}
.nav-item {
  font-size: 1.8rem;
  font-weight: $b;
}
</style>
