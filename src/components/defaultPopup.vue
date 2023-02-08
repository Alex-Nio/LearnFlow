<template>
  <div v-if="has_files" class="popup">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ["has_files"],
};
</script>

<style lang="scss" scoped>
.popup {
  width: 100%;
  max-width: 820px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 25px;
  /* From https://css.glass */
  background: rgba(163, 163, 163, 0.2);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border: 1px solid rgba(163, 163, 163, 0.3);
  animation: fadeIn 0.5s linear;
}
</style>
