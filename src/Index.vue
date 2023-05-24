<template>
    <div id="mapContainer"></div>
    <div class="toolbar">
        <a-button v-for="(item, index) in measureList" :key="index" class="toolbar-btn" type="primary"
            @click="start(item)">{{
                item.name }}</a-button>
        <a-button class="toolbar-btn" type="primary" danger @click="clear">清除</a-button>
    </div>
</template>
<script setup lang="ts">
import { onMounted, toRefs,reactive } from "vue";
import Prompt from "./js/prompt/prompt.js"
import util from "./js/util"
import Tool from "./js/measure/measureTool.js"
let viewer = undefined;

const state = reactive({
    measureList: [
        {
            name: "空间距离",
            type: "1",
            unitType: "dis",
        },
        {
            name: "贴地距离",
            type: "2",
            unitType: "dis",
        },
        {
            name: "面积",
            type: "3",
            unitType: "area",
            icon: "icon-tiedixingzhuang",
        },
        {
            name: "角度",
            type: "7",
            unitType: "",
            icon: "icon-jiaodu",
        },
        {
            name: "高度差",
            type: "4",
            unitType: "dis",
            icon: "icon-gaoducha",
        },
        {
            name: "三角测量",
            type: "5",
            unitType: "dis",
            icon: "icon-sanjiaoceliang",
        },
        {
            name: "坐标测量",
            type: "6",
            unitType: "",
            icon: "icon-zuobiaoceliang",
        }
    ]
})
const { measureList } = toRefs(state)
let measureTool = undefined;
onMounted(() => {
    viewer = new Cesium.Viewer('mapContainer', {
        imageryProvider: new Cesium.ArcGisMapServerImageryProvider({
            url: "https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer"
        }),
        terrainProvider: new Cesium.CesiumTerrainProvider({
            url: "http://data.marsgis.cn/terrain"
        }),
        animation: false,  // 设置动画小组件关闭展示
        timeline: false, // 时间轴关闭展示
        infoBox: false, // 信息盒子关闭展示
        geocoder: false, // 地理编码搜索关闭展示
        baseLayerPicker: false, // 基础图层选择器关闭展示
        sceneModePicker: false, // 场景选择器关闭展示
        fullscreenButton: false, // 全屏按钮关闭展示
        navigationInstructionsInitiallyVisible: false, // 导航说明是否最初展示
        navigationHelpButton: false, // 导航帮助按钮关闭展示
        homeButton: false
    });
    document.getElementsByClassName("cesium-viewer-bottom")[0].style.display = "none";
    util.setCameraView({
        "x": 116.98180343031277,
        "y": 31.65625287717623,
        "z": 55533.08874146516,
        "heading": 359.31730998394744,
        "pitch": -55.72609786048885,
        "roll": 359.97907544797624,
        "duration": 0
    }, viewer);
    measureTool = new Tool(viewer);
})

const start = (item: any) => {
    if (!measureTool) return;
    if (
        measureTool.nowDrawMeasureObj || measureTool.nowEditMeasureObj
    ) {
        alert("请结束当前量算");
        return;
    }

    // 开始量算
    measureTool.start({
        type: item.type,
    });
}

const clear = () => {
    if (!measureTool) return;
    measureTool.clear();
}


</script>

<style scoped>
.toolbar {
    position: absolute;
    top: 20px;
    left: 20px;
    z-index: 999;
}

.toolbar-btn {
    margin: 10px;
}

#mapContainer {
    margin: 0;
    padding: 0;
    height: 100%;
}
</style>

