<template>
  <div></div>
</template>
  
<script>

export default {
  data() {
    return {
      isActive: false,
    };
  },
  methods: {
    toggleCountryWindow() {
      this.isActive = !this.isActive;
    },
  },
};
</script>

<style scoped>
</style>
  