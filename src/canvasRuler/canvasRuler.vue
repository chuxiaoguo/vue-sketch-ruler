<template>
    <canvas class="ruler"
        ref="$canvas"
        @click="handleClick"
        @mouseenter="handleEnter"
        @mousemove="handleMove"
        @mouseleave="handleLeave"
    />
</template>
<script>
import { drawHorizontalRuler, drawVerticalRuler } from './utils';
const getValueByOffset = (offset, start, scale) => Math.round(start + offset / scale)
export default {
    name: 'CanvasRuler',
    data() {
        return {
            $canvas: {},
            canvasContext: {},
        }
    },
    props: {
        vertical: Boolean,
        start: Number,
        scale: Number,
        width: Number,
        height: Number,
        canvasConfigs: Object,
        selectStart: Number,
        selectLength: Number,
    },
    watch: {
        start() {
            this.drawRuler();
        },
        width(val) {
            this.updateCanvasContext();
            this.drawRuler();
        },
        height(val) {
            this.updateCanvasContext(); 
            this.drawRuler();
        },
    },
    methods: {
        initCanvasRef() {
            this.$canvas = this.$refs.$canvas;
            this.canvasContext = this.$canvas && this.$canvas.getContext('2d')
        },
        updateCanvasContext () {
            const { ratio } = this.canvasConfigs;
            
            // 比例宽高
            this.$canvas.width = this.width * ratio;
            this.$canvas.height = this.height * ratio;

            const ctx = this.$canvas.getContext('2d');
            ctx.font = `${12 * ratio}px -apple-system, 
                "Helvetica Neue", ".SFNSText-Regular", 
                "SF UI Text", Arial, "PingFang SC", "Hiragino Sans GB", 
                "Microsoft YaHei", "WenQuanYi Zen Hei", sans-serif`;
            ctx.lineWidth = 1;
            ctx.textBaseline = 'middle';
        },
        drawRuler() {
            const options = { 
                scale: this.scale, 
                width: this.width, 
                height: this.height, 
                canvasConfigs: this.canvasConfigs
            }
            
            if (this.vertical) {
                drawVerticalRuler(
                    this.canvasContext,
                    this.start,
                    { y: this.selectStart, height: this.selectLength },
                    options
                )
            } else {
                drawHorizontalRuler(
                    this.canvasContext, 
                    this.start, 
                    { x: this.selectStart, width: this.selectLength }, 
                    options
                )
            }
        },
        handleClick(e) {
            const offset = this.vertical ? e.offsetY : e.offsetX;
            const value = getValueByOffset(offset, this.start, this.scale);
            this.$emit('onAddLine', value); 
        },
        handleEnter(e) {
            const offset = this.vertical ? e.offsetY : e.offsetX;
            const value = getValueByOffset(offset, this.start, this.scale);
            this.$emit('onIndicatorShow', value); 
        },
        handleMove(e) {  
            const offset = this.vertical ? e.offsetY : e.offsetX
            const value = getValueByOffset(offset, this.start, this.scale);
            this.$emit('onIndicatorMove', value); 
        },
        handleLeave() {
            this.$emit('onIndicatorHide');
        }
    },
    mounted() {
        this.initCanvasRef();
        this.updateCanvasContext()
        this.drawRuler()
    }
}
</script>