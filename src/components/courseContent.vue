<template>
  <div class="course-content">
    <ul class="courses-list">
      <li class="course-list__item" v-for="item in Object.keys(category[1])">
        <router-link :to="{ name: 'Content', params: { pageName: item } }">{{
          item
        }}</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["category"],
};
</script>

<style lang="scss" scoped>
.course-list__item {
  font-size: 1.6rem;
}
</style>
