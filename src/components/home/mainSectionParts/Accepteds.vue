<template>
  <div class="container-fluid p-5" style="background: #eee">
    <div class="row">
      <div class="col-12 text-end">
        <h4>
          آخرین لیست وضعیت ارایه تاییدیه به موبایل پوزهای شبکه پرداخت کشور
        </h4>
        <p class="text-muted">
          کد خبر: SHP-93445&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ساعت انتشار:
          09:18&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; تاریخ انتشار: 1398/02/04
        </p>
      </div>
    </div>
    <hr />
    <div class="row p-5 align-items-center justify-content-center">
      <img src="../../../../public/img/accepted.png" style="width: 80%" />
    </div>
    <div class="row my-5 text-secondary fs-5 text-end">
      آخرین لیست وضعیت ارایه تاییدیه به موبایل پوزهای شبکه پرداخت کشور در فایل
      ذیل قابل دریافت است.
    </div>
    <hr />
    <div class="row py-2 align-items-center justify-content-center">
      <button class="btn btn-primary w-25">دریافت پرونده پیوست</button>
    </div>
    <div class="row text-end">
      <span class="fs-4"
        >دسته بندی:&nbsp;&nbsp;<span
          class="px-2 text-muted small fs-6"
          style="background: #ddd; width: 50px; border-radius: 5px"
          >اخبار</span
        ></span
      >
    </div>
    <hr />
    <div class="row">
      <div class="fs-4 text-end">اخبار مرتبط:</div>
      <swiper
        :width="300"
        navigation
        autoplay
        :scrollbar="{ draggable: true }"
        @swiper="onSwiper"
        @slideChange="onSlideChange"
        @mouseenter="slidehover = true"
        @mouseleave="slidehover = false"
      >
        <swiper-slide
          v-for="item in news"
          :key="item.id"
          :class="{ 'non-gray-fiter': slidehover }"
          class="mx-4 my-3"
        >
          <a href="" class="text-center text-decoration-none text-dark">
            <div>
              <img
                :src="item.img_url"
                style="
                  width: 180px;
                  height: 130px;
                  margin-right: -10px;
                  border-radius: 5px;
                "
              />
            </div>

            <h6 class="mt-3 fw-bold">{{ item.title }}</h6>
          </a>
          <div></div>
        </swiper-slide>
      </swiper>
    </div>
  </div>
</template>

<script>
import SwiperCore, {
  Navigation,
  Pagination,
  Scrollbar,
  A11y,
  Autoplay,
} from "swiper";

// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/swiper.scss";
import "swiper/components/navigation/navigation.scss";
import "swiper/components/pagination/pagination.scss";
import "swiper/components/scrollbar/scrollbar.scss";
import { computed, ref } from "@vue/reactivity";
import { useStore } from "vuex";

// install Swiper modules
SwiperCore.use([Navigation, Pagination, Scrollbar, A11y, Autoplay]);

// Import Swiper styles
export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  methods: {
    onSwiper(swiper) {
      console.log(swiper);
    },
    onSlideChange() {
      console.log("slide change");
    },
  },
  setup() {
    const store = useStore();

    fetchNews();
    const news = computed(() => store.getters["news/allNews"]);
    async function fetchNews() {
      // loading.value = true;
      await store.dispatch("news/fetchAllNews");
      // loading.value = false;
    }

    const slidehover = ref(false);
    return {
      news,
      slidehover,
    };
  },
};
</script>
<style scoped>
.non-gray-fiter {
  filter: grayscale(100%);
  -webkit-filter: grayscale(100%);
}
.non-gray-fiter:hover {
  filter: grayscale(0%);
  -webkit-filter: grayscale(0%);
}
</style>
