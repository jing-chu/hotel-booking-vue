<template>
  <div>
    <button v-if="isDark" type="button" class="mode" @click="setMode">
      Light Mode
    </button>
    <button v-else type="button" class="mode" @click="setMode">
      Dark Mode
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDark: false
    };
  },
  methods: {
    setMode: function() {
      if (this.isDark) {
        this.$colorMode.preference = "light";
        this.isDark = false;
      } else {
        this.$colorMode.preference = "dark";
        this.isDark = true;
      }
    }
  }
};
</script>

<style>
.mode {
  border: none;
  background-color: var(--bg-secondary);
  color: var(--color);
  right: 400px;
  width: 90px;
  margin-bottom: 1rem;
  text-align: left;
}
</style>
