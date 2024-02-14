<template>
  <div :class="['app-sidebar', { 'sidebar-is-active': isActive }]">
    <!-- Sidebar content goes here -->
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      isActive: false,
    };
  },
  methods: {
    toggleSidebar() {
      this.isActive = !this.isActive;
      this.$emit('update:isActive', this.isActive); // Emit an event when the sidebar toggles
    },
  },
};
</script>

<style scoped>
.app-sidebar {
  width: 30%;
  height: 91vh;
  position: fixed;
  top: 0;
  right: -100%; /* Start off the screen */
  background: #f4f4f4;
  transition: right 0.3s ease;
  z-index: 1000; /* Ensure it's above other content */
}

.sidebar-is-active {
  right: 0; /* Slide in */
}
</style>
  