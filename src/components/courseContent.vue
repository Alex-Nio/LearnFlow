<template>
  <div class="course-content">
    <ul class="courses-list">
      <li class="course-list__item" v-for="item in Object.keys(category[1])">
        <router-link
          :to="{
            name: 'Content',
            params: {
              categoryName: categoryName,
              pageName: item,
            },
          }"
          >{{ item }}</router-link
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["category", "categoryName", "pageName"],
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/imports.scss";
.course-content {
  @include fdrjc_aic;
  width: 100%;
  max-width: 820px;
  padding: 20px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 16px;
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  margin: 0 auto;
  min-height: 270px;
  transition: all 0.5s ease-out;
  box-sizing: border-box;
}
.course-list__item {
  font-size: 2.2rem;
  margin: 10px 0;
  text-align: center;
}

@media screen and (min-width: 320px) and (max-width: 768px) {
  .course-list__item {
    font-size: 1.4rem;
  }
}
</style>
