<template>
    <div class="map-wrap">
      <a href="https://www.maptiler.com" class="watermark"><img
          src="https://api.maptiler.com/resources/logo.svg" alt="MapTiler logo"/></a>
      <div class="map" ref="mapContainer"></div>
    </div>
  </template>
  
  <script >
  import { Map, NavigationControl, Marker, Popup } from 'maplibre-gl';
  import { shallowRef, onMounted, onUnmounted, markRaw } from 'vue';
  
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Map",
    setup () {
      const mapContainer = shallowRef(null);
      const map = shallowRef(null);
  
      onMounted(() => {
        const apiKey = 'YHCbRNypqwfQcI3Rb2vf';
  
        const initialState = { lng: 71.427, lat: 51.1301, zoom: 14 };
  
        map.value = markRaw(new Map({
          container: mapContainer.value,
          style: `https://api.maptiler.com/maps/streets-v2/style.json?key=${apiKey}`,
          center: [initialState.lng, initialState.lat],
          zoom: initialState.zoom
        }));
        map.value.addControl(new NavigationControl(), 'top-right');
      new Marker({color: "#FF0000"})
        .setLngLat([71.425487, 51.128426])
        .addTo(map.value);


      
       new Popup({ closeOnClick: false })
        .setLngLat([71.425487, 51.128426])
        .setHTML('<img src="https://dynamic-media-cdn.tripadvisor.com/media/photo-o/0f/ba/29/5c/img-worlds-of-adventure.jpg?w=1200&h=1200&s=1"></img><h1>Hello World!</h1>')
        .addTo(map.value);  



      }),
      onUnmounted(() => {
        map.value?.remove();
      })
  
      return {
        map, mapContainer
      };
    }
  };
  </script>
  
  
  <style scoped>
  @import '~maplibre-gl/dist/maplibre-gl.css';
  
  .map-wrap {
    position: relative;
    width: 100%;
    height: calc(100vh - 77px); /* calculate height of the screen minus the heading */
  }
  
  .map {
    position: absolute;
    width: 100%;
    height: 100%;
  }
  
  .watermark {
    position: absolute;
    left: 10px;
    bottom: 10px;
    z-index: 999;
  }
  </style>