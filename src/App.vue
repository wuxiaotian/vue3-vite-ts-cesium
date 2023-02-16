<template>
  <div id="cesiumContainer">
  </div>
</template>

<script lang="ts">
import { onMounted } from "vue";
export default {
  name: "Home",
  setup() {
    const Cesium = window.Cesium;
    let viewer;
    onMounted(() => {
      let key =
          "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJiYjUwNWQyOC0yZmZhLTRmMzItOTQyZC02ZmQyMWIyMTA3NmEiLCJpZCI6NjcyNzcsImlhdCI6MTY2ODE1ODc2Mn0.t1h6-ZADkGnZUZZoLtrlgtTp8_MR2Kxfhew42ksDgmk";
      Cesium.Ion.defaultAccessToken = key;
      viewer = window.Viewer = new Cesium.Viewer("cesiumContainer", {
        imageryProvider: new Cesium.ArcGisMapServerImageryProvider({
          url: "https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer",
        }),
        terrainProvider: Cesium.createWorldTerrain(),
        geocoder: true,
        homeButton: true,
        sceneModePicker: true,
        baseLayerPicker: true,
        navigationHelpButton: true,
        animation: false,
        timeline: false,
        fullscreenButton: false,
        vrButton: false,
        //关闭点选出现的提示框
        selectionIndicator: false,
        infoBox: false,
      });
      viewer.scene.debugShowFramesPerSecond = true;
      viewer._cesiumWidget._creditContainer.style.display = "none"; // 隐藏版权
    });
  },
};
</script>

<style lang="scss" scoped>

#cesiumContainer {
  position: relative;
  width: 100%;
  height: 100%;
  .my-Select {
    position: absolute;
    margin: 10px;
    padding: 10px;
    border: 1px solid red;
    border-radius: 4px;
    z-index: 10;
  }
}
</style>
