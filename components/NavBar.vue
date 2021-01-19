<template>
  <header class="header">
    <div class="main">
      <h1 class="title">Book A Hotel</h1>
      <ul>
        <li>
          <nuxt-link to="/">Login</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/hotels">Search</nuxt-link>
        </li>
      </ul>
    </div>
    <button style="button" class="mode">Dark Mode</button>
  </header>
</template>

<script>
export default {
  name: "NavBar",
};
</script>

<style>
.header {
  display: flex;
  flex-direction: column;
  border-bottom: 1px dotted #ccc;
}

.mode {
  border: none;
  background-color: white;
  right: 400px;
  width: 90px;
  margin-bottom: 1rem;
  text-align: left;
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