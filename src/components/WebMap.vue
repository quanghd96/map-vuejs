<template>
    <div></div>
</template>

<script lang="ts">
import GraphicsLayer from 'esri/layers/GraphicsLayer';
import Graphic from 'esri/Graphic';
import PictureMarkerSymbol from 'esri/symbols/PictureMarkerSymbol';
import PopupTemplate from 'esri/PopupTemplate';

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
        const symbol = new PictureMarkerSymbol({
            url: 'https://static.arcgis.com/images/Symbols/Shapes/BlackStarLargeB.png',
            width: '64px',
            height: '64px'
        });

        const popupTemplate = new PopupTemplate({
            title: 'Coordinates',
            content: () => {
                const template = document.createElement('template');
                template.innerHTML = '<h1>Hello</h1>';
                return template.content.firstChild;
            }
        });

        const pointGraphic = new Graphic({
            geometry: point,
            symbol: symbol,
            popupTemplate: popupTemplate
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
