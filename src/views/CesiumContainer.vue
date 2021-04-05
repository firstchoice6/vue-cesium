<template>
  <div>
    <div class="options">操作区域</div>
    <div id="cesiumContainer"></div>
  </div>
</template>

<script>
import 'cesium/Build/Cesium/Widgets/widgets.css'
import { Cartesian3, Viewer, Color, Cesium3DTileset } from 'cesium'

export default {
  name: 'CesiumContainer',
  data() {
    return {
      viewer: undefined
    }
  },
  mounted() {
    this.init()
    // this.addEntity()
  },
  methods: {
    // 初始化
    init() {
      this.viewer = new Viewer('cesiumContainer', {
        geocoder: true,
        homeButton: true,
        sceneModePicker: true,
        baseLayerPicker: true,
        navigationHelpButton: true,
        animation: true,
        timeline: true,
        fullscreenButton: true,
        vrButton: true
      })
      this.viewer.scene.debugShowFramesPerSecond = false
      this.viewer._cesiumWidget._creditContainer.style.display = 'none'
    },
    // 添加实体
    addEntity() {
      this.viewer.entities.add({
        name: 'Red box with black outline',
        position: Cartesian3.fromDegrees(-107.0, 40.0, 300000.0),
        box: {
          dimensions: new Cartesian3(400000.0, 300000.0, 500000.0),
          material: Color.RED.withAlpha(0.5),
          outline: true,
          outlineColor: Color.BLACK
        }
      })
      this.viewer.zoomTo(this.viewer.entities)
    },
    // 添加3D title
    add3Dtitle() {
      const url = ''
      const modelMatrix = []
      this.viewer.scene.primitives.add(
        new Cesium3DTileset({
          url, // 数据路径
          maximumScreenSpaceError: 2, // 最大的屏幕空间误差
          maximumNumberOfLoadedTiles: 1000, // 最大加载瓦片个数
          modelMatrix // 形状矩阵
        })
      )
    }
  }
}
</script>
<style scoped>
.options {
  background-color: #12314233;
  line-height: 100px;
  text-align: center;
  width: 800px;
  height: 100px;
  position: fixed;
  z-index: 999;
}
#cesiumContainer {
  width: 100vw;
  height: 100vh;
}
</style>
