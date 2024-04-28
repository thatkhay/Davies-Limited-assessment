<template>
  <div class="theme-switch">
    <label for="theme">Theme:</label>
    <select id="theme" v-model="theme" @change="$emit('theme-changed', theme)">
      <option value="light">Light</option>
      <option value="dark">Dark</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      theme: 'light', // Set default theme to light
    };
  },
  methods: {
    emitThemeChange() {
      this.$emit('theme-changed', this.theme);
    },
  },
};
</script>

<style scoped>
.theme-switch {
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
}

label {
  margin-right: 1rem;
}

select {
  padding: 5px;
  border: 1px solid #ddd;
  border-radius: 3px;
}
</style>
