<script lang="ts">
import { defineComponent, defineEmits, inject, onMounted, PropType, reactive, ref, toRef, toRefs, onBeforeMount } from "vue";
import L, { Map, Layer, TileLayer } from 'leaflet';

import BaseMaps from "../components/map/layers/BaseMaps.vue";

import GeoJsonLayer from "../components/map/layers/GeoJsonLayer.vue";

import ParcelData from '../data/dawson_2023.json';


import 'leaflet-basemaps/L.Control.Basemaps.js';
import 'leaflet-basemaps/L.Control.Basemaps.css';
import 'leaflet/dist/leaflet.css';


const center = [32.191764, -83.951707]
const zoom = 15
const minZoom = 10
const maxZoom = 22


const geoJson = ref(ParcelData);


export default defineComponent({
    emits: ['created', 'removed'],
    components: { BaseMaps, GeoJsonLayer },
    setup(props, { emit }) {

        const container = ref<HTMLElement>();
        const map = ref<any | undefined>(null);
        function initMap() {
            console.log("initializing map...")
            console.log({ map, container });
            map.value = new L.Map(container.value || "map", {
                // preferCanvas: true,
                scrollWheelZoom: true,
            }).setView(center, zoom);


        };

        onMounted(() => {
            initMap();

        });
        // onBeforeMount(() => initMap());
        // initMap();
        const addMapLayer = (layer: any) => {
            console.log({ layer, map, val: map.value });
            layer.addTo(map.value);
            zoomToLayer(layer);

        }

        const zoomToLayer = (layer: any) => {
            console.log({ layer });
            const layerBounds = layer.getBounds();

            // map.fitBounds(layerBounds);
            map.value?.flyToBounds(layerBounds);
        }


        return {
            map,
            geoJson,
            container,
            addMapLayer,
        };
    }
});

</script>

<template>
    <div class="container-fluid">
        <div class="row">
            <h1>Welcome to the GIS Map</h1>
        </div>
        <div class="row">
            <div ref="container" id="map" class="col-12 full-height">
                <div v-if="map">
                    <BaseMaps :map="map" />
                    <GeoJsonLayer :map="map" :geoJson="geoJson" @layerCreated="addMapLayer" />
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#map {
    min-height: 75vh;
    width: 100%;
}
</style>