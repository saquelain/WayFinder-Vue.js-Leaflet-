<template>
    <div id="map" class="my-component">
        <button class="close-btn" @click="closeComponent">X</button>
    </div>
    
  </template>

  <script>
  import L from 'leaflet';
  
  export default {
    name: 'MapComp',
    mounted() {

        const latitude = parseFloat(localStorage.getItem('latitude')) || 51.505;
        const longitude = parseFloat(localStorage.getItem('longitude')) || -0.09;   

      this.map = L.map('map').setView([latitude, longitude], 14);
  
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; OpenStreetMap contributors'
      }).addTo(this.map);
  
      const markerIcon = L.icon({
        iconUrl: 'https://www.iconpacks.net/icons/1/free-pin-icon-48-thumb.png',
        iconSize: [25, 30],
        iconAnchor: [12, 29],
        popupAnchor: [1, -34],
      });
  
      const marker = L.marker([latitude, longitude], { icon: markerIcon }).addTo(this.map);
  
      marker.bindPopup(`<h1>Location:</h1> <h2>${localStorage.getItem('locationName')}<h2> <hr> <h1>Description:</h1> <h3>${localStorage.getItem('description')}<h3>`);
    },

    methods: {
    closeComponent() {
      this.$emit('close');
    }
  }
  }
  </script>
  
  <style>
  #map {
    height: 600px;
    margin-left: 30px;
    margin-right: 30px;
  }

  .my-component {
  position: relative;
}


  .close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: transparent;
  border: none;
  color: #000;
  font-size: 24px;
  cursor: pointer;
  z-index: 1000;
  font-weight: bold;
}

.close-btn:hover::after {
  content: "close";
  position: absolute;
  bottom: -20px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 13px;
}
  </style>
  