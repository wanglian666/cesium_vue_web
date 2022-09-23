<template>
    <div class="box" id="viewerContainer" style="width: 100%; height: 100%"></div>
  </template>
  
  <script lang="ts">
  import { onMounted } from "vue";
  import * as Cesium from "cesium";
  export default {
    name:"home",
    setup() {
      onMounted(() => {
        initViewer();
      });
      const initViewer = () => {
        var esriMap = new Cesium.ArcGisMapServerImageryProvider({
          url: "https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer",
          enablePickFeatures: false,
        });
        Cesium.Ion.defaultAccessToken =
          "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwNzlhZDRlYy1kY2ZlLTQwMDEtOTExMS1lYjhkZTQyZjkyODkiLCJpZCI6MTA4NDQ4LCJpYXQiOjE2NjM1Njk5OTV9.x-Rk2pcM8enrmUOJtWehE5EbKEpT8uCiOEh79J-6Log";
        var worldTerrain = Cesium.createWorldTerrain({
          requestWaterMask: true,
          requestVertexNormals: true,
        });
        const viewer = new Cesium.Viewer("viewerContainer", {
          animation: false, //是否创建动画小器件，左下角仪表
          timeline:false,
          navigationHelpButton:false,
          baseLayerPicker: false, //是否显示图层选择器
          fullscreenButton: false, //是否显示全屏按钮
          geocoder: false, //是否显示geocoder小器件，右上角查询按钮
          // homeButton: false, //是否显示home按钮
          infoBox: false, //是否显示信息框
          sceneModePicker: false, //是否显示3D/2D选择器
          imageryProvider: esriMap,
          terrainProvider: worldTerrain,
        });
        viewer.scene.globe.show = true; // 地球显示隐藏
        viewer.cesiumWidget.creditContainer.style.display = "none";
        Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(90, -20, 110, 90);
      };
    },
  };
  </script>
  
  <style lang="scss" scoped>
    .box {
      width: 100%;
      height: 100%;
    }
  </style>