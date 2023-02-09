<template>
  <div class="search">
    <div class="search-box">
      <label for="search"></label>
      <input
        :value="searchQuery"
        @input="updateSearchQuery"
        class="search-input"
        id="search"
        name="search"
        type="search"
        placeholder="Найти"
      />
      <button type="submit" class="searchButton">
        <img src="./../assets/img/search-btn.gif" alt="" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["searchQuery"],
  data() {
    return {
      active: false,
    };
  },
  methods: {
    updateSearchQuery(event) {
      this.$emit("update:searchQuery", event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.search {
  position: fixed;
  top: 13px;
  right: -80px;
  width: 100%;
  max-width: 610px;
  margin: 0 auto;
  justify-self: flex-end;
}
.search-input {
  position: relative;
  width: 100%;
  max-width: 400px;
  padding: 15px 45px 15px 15px;
  border: 1px solid #fefefe;
  border-radius: 5px 0 0 5px;

  &::after {
    position: absolute;
    content: "";
    top: 50%;
    right: 22px;
    transform: translateY(-50%);
    width: 12px;
    height: 12px;
  }
}

.search-box {
  display: flex;
  align-items: center;
  overflow: hidden;
}

.searchButton {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 48px;
  background: #ffffff;
  text-align: center;
  color: #fff;
  border-radius: 0 5px 5px 0;
  font-size: 20px;

  & img {
    width: 30px;
  }
}

.search-result-wrapper {
  display: flex;
  flex-direction: column;
  padding: 25px;
  margin: 40px 0 0 0;
  overflow: hidden;
  max-height: 120px;
  background: rgba(255, 255, 255, 0.7);
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
  border-radius: 1rem;
  animation: slideInUp 0.3s linear;
}
.search-result {
  border-radius: 1rem;
}
.search-result-item {
  font-size: 2rem;
  margin: 2px 0;
}
</style>
