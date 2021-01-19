<template>
  <div class="container">
    <NavBar />
    <Nuxt />
  </div>
</template>

<script>
import NavBar from "../components/NavBar";

export default {
  components: {
    NavBar
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

a {
  color: #666;
  text-decoration: none;
}

ul {
  list-style: none;
}

.container {
  max-width: 800px;
  height: auto;
  margin: 2rem auto;
  overflow: hidden;
  padding: 1rem 2rem;
  background: var(--bg-secondary);
}
</style>
