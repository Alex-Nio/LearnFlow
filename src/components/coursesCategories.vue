<template>
  <swiper
    :direction="'vertical'"
    :slides-per-view="5"
    :centeredSlides="true"
    :spaceBetween="25"
    :loop="true"
    :mousewheel="true"
    :pagination="{
      clickable: true,
    }"
    :modules="modules"
    @swiper="onSwiper"
    @slideChange="onSlideChange"
    class="mySwiper"
  >
    <swiper-slide class="courses" v-for="(category, index) in this.courses.categories">
      <div @click="openCategory(category, index)" class="course-title">
        {{ category[0] }}
      </div>
    </swiper-slide>
  </swiper>
</template>

<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";

import "swiper/css/pagination";

// import required modules
import { Mousewheel, Pagination } from "swiper";

export default {
  props: ["courses"],
  emits: ["open"],
  components: {
    Swiper,
    SwiperSlide,
  },
  methods: {
    openCategory(category, index) {
      this.$emit("open", category, index);
    },
  },
  setup() {
    // Slide Content Toggle
    function slideContentToggle(slideSelector, courseTitle) {
      let x = document.querySelector(slideSelector).querySelector(courseTitle);
      x.click();
    }

    const onSwiper = (swiper) => {
      slideContentToggle(".swiper-slide-active", ".course-title");
    };
    const onSlideChange = (swiper) => {
      console.log("slide change");

      document.addEventListener("wheel", (event) => {
        // Move down / up wheel
        if (event.deltaY > 0) {
          slideContentToggle(".swiper-slide-active", ".course-title");
        } else {
          slideContentToggle(".swiper-slide-active", ".course-title");
        }
      });
    };
    return {
      onSwiper,
      onSlideChange,
      modules: [Mousewheel, Pagination],
    };
  },
};
</script>

<style lang="scss" scoped>
$slider-max-height: 270px;

.course-title {
  font-size: 3.6rem;
  text-align: center;
  cursor: pointer;
}

.swiper {
  width: 100%;
  height: 100%;
  max-height: $slider-max-height;
  overflow: hidden !important;
  background: transparent;
}

.swiper-slide {
  text-align: center;
  max-height: $slider-max-height;
  font-size: 18px;
  color: rgba(164, 163, 164, 0.629);
  display: flex;
  justify-content: center;
  align-items: center;
}

.swiper-slide-active {
  color: #000;
}

.swiper-slide img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
