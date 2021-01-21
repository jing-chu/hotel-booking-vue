<template>
  <div class="main_container">
    <img
      src="/color_logo_no_background.png"
      alt="logo"
      width="400"
      height="100"
    />
    <form class="form" @submit.prevent="submitForm">
      <div class="form-control">
        <label class="email">Email:</label>
        <input id="email" type="text" />
      </div>
      <div class="form-control">
        <label class="password">Password:</label>
        <input id="password" type="text" />
      </div>
      <nuxt-link to="/hotels">
        <button type="submit" @click="handleLogout" class="btn">Login</button>
      </nuxt-link>
    </form>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "Login",
      meta: [
        {
          hid: "hotel searching and booking",
          nane: "hotel searching and booking",
          content: "Best place for hotel searching and booking"
        }
      ]
    };
  },

  methods: {
    handleLogout: function() {
      this.$nuxt.$emit("show-logout", true);
    }
  }
};
</script>

<style>
.main_container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 1rem;
}
.form {
  background: var(--bg);
  max-width: 450px;
  margin: 0 auto;
  margin-bottom: 4rem;
  padding: 1rem 2rem;
  border-radius: 0.25rem;
}
.form input {
  background: hsl(210, 36%, 96%);
  border-color: transparent;
  border-radius: 0.25rem;
  padding: 0.25rem 0.5rem;
}
.form-control {
  margin: 0.5rem 0;
  display: grid;
  grid-template-columns: 100px 1fr;
  align-items: center;
}
.form button {
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
