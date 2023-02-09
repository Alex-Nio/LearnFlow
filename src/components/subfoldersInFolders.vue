<template>
  <div class="sub-folders-more">
    <div v-for="(item, i) in filtredSubFiles">
      <p class="sub-folders-more__item">{{ item[i] }}</p>
    </div>
  </div>
</template>

<script>
export default {
  //   TODO: filtredSubFolders это массив с подпапками внутри подпапки, props оставлен как напоминание
  props: ["filtredSubFiles", "filtredSubFolders"],
};
</script>

<style lang="scss" scoped>
.sub-folders-more {
  &__item {
    font-size: 1.4rem;
  }
}
</style>
