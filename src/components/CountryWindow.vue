<template>
   <div id="sliding-window">
    <div id="window-header">
      <button class="country-close-btn" @click="closeCountryWindow">x</button>
    </div>
    <div id="window-content">
        <h2 id="country-name">Country Name</h2>
        <!-- Additional content here -->
    </div>
  </div>
</template>
  
<script>

export default {
  data() {
    return {
      // to add
    };
  },
  methods: {
    closeCountryWindow() {
      document.getElementById('sliding-window').classList.remove('active');
    }
  },
};
</script>

<style scoped>
#window-header {
    display: flex; /* Use flexbox for easy alignment */
    justify-content: flex-end; /* Align the button to the right */
    padding: 10px; /* Add some padding around the button */
}
.country-close-btn{
  position: relative; /* Fixed position relative to the viewport */
  top: 10px; /* Distance from the top of the viewport */
  right: 10px; /* Distance from the right of the viewport */
  z-index: 1050; /* Ensures the button is above most other content */
  
  /* Styling the button for better visibility */
  padding: 0.5em 1em;
  background-color: #007bff; /* Example button color */
  color: #ffffff; /* Text color */
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.country-close-btn.hover{
  background-color: #0056b3; /* Darker shade for hover state */
}

/* Sliding window styles */
#sliding-window {
    position: fixed;
    left: -100%; /* Start off-screen */
    top: 0;
    width: 65%; /* Adjust width as needed */
    height: 91vh;
    background-color: white;
    box-shadow: 2px 0 5px rgba(0,0,0,0.5);
    transition: left 0.3s ease;
    z-index: 1000;
}

/* When active, slide in */
#sliding-window.active {
    left: 0;
}
</style>
  