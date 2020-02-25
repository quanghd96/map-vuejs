<template>
    <div></div>
</template>

<script lang="ts">
import GraphicsLayer from 'esri/layers/GraphicsLayer';
import Graphic from 'esri/Graphic';

export default {
    name: 'WebMap',
    async mounted() {
        const app = await import('../data/map');
        const graphicsLayer = new GraphicsLayer();
        app.webmap.add(graphicsLayer);
        const point = {
            type: 'point',
            longitude: 105.8194541,
            latitude: 21.0227788
        };
        const simpleMarkerSymbol = {
            type: 'picture-marker', // autocasts as new PictureMarkerSymbol()
            url: 'https://static.arcgis.com/images/Symbols/Shapes/BlackStarLargeB.png',
            width: '64px',
            height: '64px'
        };

        const pointGraphic = new Graphic({
            geometry: point,
            symbol: simpleMarkerSymbol
        });

        graphicsLayer.add(pointGraphic);
        app.initialize(this.$el);
    }
};
</script>

<style lang="scss" scoped>
div {
    padding: 0;
    margin: 0;
    width: 100%;
    height: 100%;
}
</style>
