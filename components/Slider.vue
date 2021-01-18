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
  cursor: pointer;
  top: 40%;
  width: auto;
  padding: 5px;
  color: white;
  background-color: rgba(0, 0, 0, 0.9);
  font-weight: bold;
  font-size: 14px;
  transition: 0.7s ease;
  border-radius: 0 4px 4px 0;
  text-decoration: none;
  user-select: none;
}
</style>