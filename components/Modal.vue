<template>
  <div class="modal" v-show="value">
    <div class="modal-container">
      <p>Please confirm your booking</p>
      <nuxt-link to="../hotels/">
        <button>Confirm</button>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    value: {
      required: true,
    },
  },
};
</script>

<style>
.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
</style>