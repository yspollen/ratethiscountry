<template>
  <button class="sidebar-toggle-btn" :class="{ 'sidebar-button-active': isSidebarActive }" @click="toggleSidebar">☰</button>
  <AppSidebar @update:isActive="isSidebarActive = $event" ref="sidebarRef" />
  <CountryWindow ref="countryWindowRef" />
  <div id="map" style="height: 90vh; width: 100vw;"></div>
  <div id="ad" style="height: 10vh; width: 100vw;"><br>Your ad goes here</div>
</template>

<script>
import { onMounted } from 'vue';
import L from 'leaflet';
import countries from './assets/geojson/countries.json'; // GeoJSON data acquired from https://geojson-maps.ash.ms/
import AppSidebar from './components/AppSidebar.vue';
import CountryWindow from './components/CountryWindow.vue';

export default {
  name: 'App',
  setup() {
    onMounted(() => {
      // render the world map
      const map = L.map('map').setView([48.8566, 2.3522], 2);
      // countries landscape
      const url = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png';
      const attribution = 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors';
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        url: url,
        attribution: attribution
      }).addTo(map);
      // countries borders
      L.geoJson(countries, {
        onEachFeature: function(feature, layer) {
          layer.on('click', function() {
            openCountryWindow(feature.properties.name, feature.properties.sov_a3);
          });
        }
      }).addTo(map);
    });
  },
  components: {
    AppSidebar,
    CountryWindow
  },
  methods: {
    toggleSidebar() {
      this.$refs.sidebarRef.toggleSidebar();
    }
  }
}

function openCountryWindow(countryName, countryId) {
  document.getElementById('country-name').textContent = countryName + ", " + countryId;
  document.getElementById('sliding-window').classList.add('active');
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  height: 100vh;
  width: 100vw;
}

.sidebar-toggle-btn {
  position: fixed; /* Fixed position relative to the viewport */
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

/* Optional: Add styles for hover effect */
.sidebar-toggle-btn:hover {
  background-color: #0056b3; /* Darker shade for hover state */
}

.sidebar-button-active {
  right: 310px;
  transition: right 0.3s ease;
}
</style>
