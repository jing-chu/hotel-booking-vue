<template>
  <div>
    <div cass="imgSlider">
      <div v-for="i in [currentIndex]" :key="i">
        <img class="hotelImg" :src="currentImg" />
      </div>
      <a class="prev" @click="prev" href="#">&#10094; Previous</a>
      <a class="next" @click="next" href="#">&#10095; Next</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Slider",
  props: ["id", "hotel", "hotelImages"],

  data() {
    return {
      timer: null,
      currentIndex: 1,
    };
  },

  mounted: function () {
    this.startSlide();
  },

  methods: {
    startSlide: function () {
      this.next;
    },

    next: function () {
      this.currentIndex += 1;
    },

    prev: function () {
      this.currentIndex -= 1;
    },
  },

  computed: {
    currentImg: function () {
      return this.hotelImages[
        Math.abs(this.currentIndex) % this.hotelImages.length
      ];
    },
  },
};
</script>

<style>
.prev,
.next {
  display: inline-block;
  background: #333;
  color: #fff;
  border-color: transparent;
  margin-top: 1rem;
  text-transform: capitalize;
  border-radius: 0.25rem;
  cursor: pointer;
  border-radius: 0.25rem;
  padding: 0.3rem 1rem;
}
</style>