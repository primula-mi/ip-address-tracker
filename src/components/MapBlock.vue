<script setup>
// import {LMap, LTileLayer, LMarker, LTooltip } from "leaflet";
import { onMounted, onUpdated } from 'vue';
import L from "leaflet";

const props = defineProps(['mapData']);
console.log("mapData: ", props.mapData);
let mainMap;
let customIcon = L.icon({
    iconUrl: '/src/assets/images/icon/icon-location.svg'
});
const buildMap = (latitude, longitude) => {
    
    mainMap = L.map('map').setView([latitude, longitude], 13);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 15,
        attribution: '© OpenStreetMap'
    }).addTo(mainMap);
    
    L.marker([latitude, longitude], {icon: customIcon}).addTo(mainMap);
}

// buildMap(props.mapData[0], props.mapData[1]);

onMounted(() => {
    buildMap(props.mapData[0], props.mapData[1]);
});
onUpdated(() => {
    mainMap = L.map('map').setView([props.mapData[0], props.mapData[1]], 13);
    L.marker([props.mapData[0], props.mapData[1]], {icon: customIcon}).addTo(mainMap);
    // buildMap(props.mapData[0], props.mapData[1]);
});

</script>
<template>
    <div id="map"></div>
</template>

<style scoped>
    #map  { 
        height: 80vh;
        width: 100%;
        z-index: 1;
        position: relative;
        overflow: hidden;
    }
    @media(max-width: 375px) {
        #map {
            height: 100vh;
        }
    }
</style>