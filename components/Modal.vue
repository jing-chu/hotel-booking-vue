<template>
  <div class="modal" v-show="value">
    <div class="modal-container">
      <p>You have successfully booked the hotel.</p>
      <nuxt-link to="../hotels/">
        <button class="button">OK</button>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    value: {
      required: true
    }
  }
};
</script>

<style>
.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: var(--bg);
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-container button {
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
