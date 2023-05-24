<script setup>
import "leaflet/dist/leaflet.css";
import { LMap, LTileLayer, LMarker, LIcon } from "@vue-leaflet/vue-leaflet";
import customIcon from '@/assets/images/icon/icon-location.svg'

const props = defineProps(['mapData']);
const zoom = 15;
const staticAnchor = [16, 37];
const iconSize = [32, 37];
</script>

<template>
    <div id="map">
      <l-map ref="map" v-model:zoom="zoom" :center="[props.mapData[0], props.mapData[1]]">
        <l-tile-layer
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
          layer-type="base"
          name="OpenStreetMap"
        ></l-tile-layer>
        <l-marker :lat-lng="[props.mapData[0], props.mapData[1]]" >
            <l-icon
                :icon-size="iconSize"
                :icon-anchor="staticAnchor"
                :icon-url="customIcon" >
            </l-icon>
        </l-marker>
      </l-map>
    </div>
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