<template>
  <header class="header">
    <div class="main">
      <h1 class="title">Book A Hotel</h1>
      <ul>
        <li>
          <nuxt-link v-if="showLogout" to="/hotels">Search</nuxt-link>
        </li>
        <li v-if="showLogout" @click="hideLogout">
          <nuxt-link to="/">Logout</nuxt-link>
        </li>
      </ul>
    </div>
    <ModePicker />
  </header>
</template>

<script>
import ModePicker from "../components/ModePicker";

export default {
  name: "NavBar",

  data() {
    return {
      showLogout: false
    };
  },

  components: {
    ModePicker
  },

  created() {
    this.$nuxt.$on("show-logout", value => {
      this.showLogout = value;
    });
  },

  methods: {
    hideLogout: function() {
      this.showLogout = false;
    }
  }
};
</script>

<style>
.header {
  display: flex;
  flex-direction: column;
  border-bottom: 1px dotted #ccc;
}

.main {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding-bottom: 1rem;
}

.title {
  font-size: 3rem;
  color: #526488;
}

.main ul {
  display: flex;
}

.main a {
  display: inline-block;
  background: #333;
  color: #fff;
  border-radius: 0.25rem;
  padding: 0.3rem 1rem;
  margin-right: 0.5rem;
}
</style>
