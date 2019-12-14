<template>
    <div class="wrapper">
        <SketchRule
            :lang="lang"
            :thick="thick"
            :scale="scale"
            :width="582"
            :height="482"
            :startX="startX"
            :startY="startY"
            :shadow="shadow"
            :horLineArr="lines.h"
            :verLineArr="lines.v"
            :cornerActive="true"
            @handleLine="handleLine"
            @onCornerClick="handleCornerClick"
        >
        </SketchRule>
        <div
            ref='screensRef'
            id="screens"
            @wheel="handleWheel"
            @scroll="handleScroll"
        >
            <div ref="containerRef" class="screen-container">
                <div id="canvas" :style="canvasStyle" />
            </div>
        </div>
    </div>
</template>
<script>
import Vue from 'vue';
import SketchRule from "vue-sketch-ruler";
const rectWidth = 160;
const rectHeight = 200;
export default Vue.extend({
    data() {
        return {
            scale: 2, //658813476562495, //1,
            startX: 0,
            startY: 0,
            lines: {
                h: [100, 200],
                v: [100, 200]
            },
            thick: 20,
            lang: "zh-CN", // 中英文
            isShowRuler: true, // 显示标尺
            isShowReferLine: true // 显示参考线
        }
    },
    components: {
        SketchRule
    },
    computed: {
        shadow() {
            return {
                x: 0,
                y: 0,
                width: rectWidth,
                height: rectHeight
            }
        },
        canvasStyle() {
            return {
                width: rectWidth,
                height: rectHeight,
                transform: `scale(${this.scale})` 
            }
        }
    },
    methods: {
        handleLine(lines) {
            this.lines = lines;
        },
        handleCornerClick() {
            return;
        },
        handleScroll() {
            const screensRect = document
                .querySelector("#screens")
                .getBoundingClientRect();
            const canvasRect = document
                .querySelector("#canvas")
                .getBoundingClientRect();

            // 标尺开始的刻度
            const startX = (screensRect.left + this.thick - canvasRect.left) / this.scale;
            const startY = (screensRect.top + this.thick - canvasRect.top) / this.scale;
            
            this.startX = startX;
            this.startY = startY;
        },
        // 控制缩放值
        handleWheel(e) {
            if (e.ctrlKey || e.metaKey) {
                e.preventDefault();
                const nextScale = parseFloat(
                    Math.max(0.2, this.scale - e.deltaY / 500).toFixed(2)
                );
                this.scale = nextScale;
            }
            this.$nextTick(() => {
                this.handleScroll();
            });
        },
    },
    mounted() {
        // 滚动居中
        this.$refs.screensRef.scrollLeft =
        this.$refs.containerRef.getBoundingClientRect().width / 2 - 300; // 300 = #screens.width / 2
    }
});
</script>
<style>
body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  overflow: hidden; }

body * {
  box-sizing: border-box;
  user-select: none; }

.wrapper {
  background-color: #f5f5f5;
  position: absolute;
  top: 100px;
  left: 100px;
  width: 600px;
  height: 500px;
  border: 1px solid #DADADC; }

#screens {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: auto; }

.screen-container {
  position: absolute;
  width: 5000px;
  height: 3000px; }

.scale-value {
  position: absolute;
  left: 0;
  bottom: 100%; }

.button {
  position: absolute;
  left: 100px;
  bottom: 100%; }

.button-ch {
  position: absolute;
  left: 200px;
  bottom: 100%; }
.button-en {
  position: absolute;
  left: 230px;
  bottom: 100%; }

#canvas {
  position: absolute;
  top: 80px;
  left: 50%;
  margin-left: -80px;
  width: 160px;
  height: 200px;
  background: lightblue;
  transform-origin: 50% 0; }
</style>