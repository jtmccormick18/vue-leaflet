
<script>
import L from "leaflet";
import { defineComponent, reactive, ref } from "vue";

// import L from 'leaflet';
// import type { PropType } from "vue";

var geojsonStyle = {
    fillColor: "#ff0000",
    color: "#000",
    weight: 1,
    opacity: 1,
    fillOpacity: 0.7,
};

var defaultOptions = {
    maxZoom: 25,
    minZoom: 1,
    tolerance: 3,
    debug: 0,
    zIndex: 401,
    style: geojsonStyle
};

function forEachFeature(feature, layer) {

    if (feature.properties) {
        layer.bindPopup(`<div>${feature.properties.PARCELID}</div>`)
    }
}


export default defineComponent({
    // components: { StarFilled },
    props: { geoJson: { required: true }, forEachFeature },
    emits: ["layerCreated"],
    setup(props, context) {
        const map = ref(props.map);
        const geoJson = ref(props.geoJson);

        console.log({ props, map, geoJson });

        const geoLayer = L.geoJSON(geoJson.value, {
            ...defaultOptions,
            onEachFeature: props.forEachFeature || forEachFeature
        })

        // geoLayer.addTo(map.value);

        context.emit("layerCreated", geoLayer);

        return {
            geoJson
        }
    },
    render() {
        // return this.$scopedSlots.default({})
    },
})
</script>

<!-- <template></template> -->

