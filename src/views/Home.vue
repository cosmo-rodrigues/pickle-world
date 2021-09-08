<template>
  <div class="hero">
    <div class="hero-body text-center d-flex">
      <h1>The Pickle World</h1>
      <div class="carousel-app d-flex">
        <Carousel
          :count="count"
          @countPlus="increment"
          @countMinor="decrement"
          :slides="slides"
        >
          <CarouselSlide
            v-for="(slide, index) in slides"
            class="carousel-slider"
            :key="slide.id"
            :index="index"
            :count="count"
          >
            <img :src="slide.image" :alt="slide.name" />
          </CarouselSlide>
        </Carousel>
      </div>
      <div class="text-center">
        <p>Developed by Cosmo Rodrigues using The Rick and Morty API from</p>
        <a
          class="text-light"
          target="_blank"
          rel="noopener noreferrer"
          href="https://axelfuhrmann.com/"
        >
          Axel Fuhrmann
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapState } from "vuex";
import Carousel from "../components/carousel/Carousel.vue";
import CarouselSlide from "../components/carousel/CarouselSlide.vue";
export default {
  name: "Home",
  data() {
    return {
      count: 0,
      slides: [],
    };
  },
  components: {
    Carousel,
    CarouselSlide,
  },
  methods: {
    ...mapActions(["getChactersImages"]),
    increment() {
      this.count++;
      if (this.count > 19) {
        this.count = 0;
      }
      this.slideDirection = "slide-right";
    },
    decrement() {
      this.count--;
      if (this.count < 1) {
        this.count = 19;
      }
      this.slideDirection = "slide-left";
    },
    checkSlide(event) {
      if (event.keyCode === 39) {
        this.increment();
      } else if (event.keyCode === 37) {
        this.decrement();
      } else {
        return;
      }
    },
  },
  computed: {
    ...mapState(["characters"]),
  },
  async mounted() {
    await this.getChactersImages();
    setTimeout(() => {
      this.characters.images?.map((el, index) => {
        this.slides.push({
          id: el.id,
          image: el.image,
          name: el.name,
          index,
        });
      });
    }, 500);
  },
};
</script>
<style>
.carousel-app {
  border-radius: 50px;
  box-shadow: -18px 3px 15px 50px #2fbd03;
  display: flex;
  height: 40vh;
  justify-content: center;
  width: 80vh;
}
.carousel-p {
  overflow: hidden;
  position: relative;
  width: 800px;
  z-index: 10;
}
.btn-p {
  background-color: #2fbd03;
  padding: 5px 10px;
  border: 1px solid transparent;
  color: #fff !important;
  height: 50px;
  margin: 5px 10px;
  margin-top: -25px;
  position: absolute;
  width: 50px;
  z-index: 2;
}
.btn-p:hover {
  color: #232c3b !important;
  cursor: pointer;
}
.btn-p:focus {
  outline: none;
}
.btn-next-p {
  top: 50%;
  right: 0;
}
.btn-prev-p {
  left: 0;
  top: 50%;
}
.carousel-slider {
  background-color: #232c3b;
  border-radius: 50px;
  bottom: 0;
  height: 40vh;
  left: 0;
  position: absolute;
  top: 0;
  right: 0;
}
.carousel-slider img {
  height: 100%;
}
.hero-body {
  align-items: center;
  justify-content: space-between;
  flex-flow: column nowrap;
}
h1 {
  padding-bottom: 20px !important;
}
</style>
