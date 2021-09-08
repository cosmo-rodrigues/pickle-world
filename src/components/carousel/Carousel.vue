<template>
  <!--

  Carousel desenveloped by:
  
  https://github.com/Aliens-dev/carousel-vue/tree/master/src
  -->
  <div class="carousel-p" @keydown="checkSlide($event)" tabindex="1 ">
    <slot></slot>
    <button @click="$emit('countPlus')" class="btn-p btn-next-p">
      <i class="fa fa-angle-right"></i>
    </button>
    <button @click="$emit('countMinor')" class="btn-p btn-prev-p">
      <i class="fa fa-angle-left"></i>
    </button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      slideDirection: "",
    };
  },
  props: {
    count: {
      type: Number,
      required: true,
    },
    slides: {
      type: Array,
      required: true,
    },
  },
  methods: {
    autoSlider() {
      setInterval(() => {
        this.$emits("countPlus");
      }, 1000);
    },
  },
  mounted() {
    this.autoSlider();
  },
  emits: ["countPlus, countMinor"],
};
</script>
<style></style>
