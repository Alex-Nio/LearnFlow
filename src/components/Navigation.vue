<template>
  <header class="header">
    <nav class="nav">
      <router-link class="nav-item" to="/">
        <span>На главную</span>
        <img src="../assets/img/home.png" alt="" />
      </router-link>
      <nav-search v-model:searchQuery="searchQuery"></nav-search>
      <!-- <div class="search-result-wrapper">
        <div class="search-result" :key="item">
          <div class="search-result-item">
            <a @click.prevent="foundItem">{{ item }}</a>
          </div>
        </div>
      </div> -->
    </nav>
  </header>
</template>

<script>
import navSearch from "@/components/navSearch";
export default {
  data() {
    return {
      searchQuery: "",
    };
  },
  components: {
    navSearch,
  },
};
</script>

<style lang="scss" scoped>
.nav {
  position: relative;
}
.nav-item {
  display: flex;
  align-items: center;
  justify-content: center;

  & span {
    margin-right: 5px;
  }

  & img {
    width: 46px;
    height: 46px;
    padding-bottom: 4px;
  }

  &:hover {
    color: #ee9b00;
  }
}
</style>
