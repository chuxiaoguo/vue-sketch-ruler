<template>
    <div class="style-ruler mb-ruler" id="mb-ruler">
        <!-- 水平方向 -->
        <RulerWrapper
            :vertical="false"
            :width="width"
            :height="thick"
            :isShowReferLine="isShowReferLine"
            :thick="thick"
            :start="startX"
            :lines="horLineArr"
            :selectStart="shadow.x"
            :selectLength="shadow.width"
            :scale="scale"
            :palette="palette"
            :canvasConfigs="canvasConfigs"
            @onLineChange="handleLineChange"
        />
        <!-- 竖直方向 -->
        <RulerWrapper
            :vertical="true"
            :width="thick"
            :height="height"
            :isShowReferLine="isShowReferLine"
            :thick="thick"
            :start="startY"
            :lines="verLineArr"
            :selectStart="shadow.y"
            :selectLength="shadow.height"
            :scale="scale"
            :palette="palette"
            :canvasConfigs="canvasConfigs"
            @onLineChange="handleLineChange"
        />
        <a 
            class="corner"
            :class="cornerActiveClass"
            :style="cornerStyle"
            @click="onCornerClick"
        ></a>
    </div>
</template>

<script>
import RulerWrapper from './rulerWrapper.vue';
const DEFAULTMENU = {
    bgColor: '#fff',
    dividerColor: '#DBDBDB',
    listItem: {
        textColor: '#415058',
        hoverTextColor: '#298DF8',
        disabledTextColor: 'rgba(65, 80, 88, 0.4)',
        bgColor: '#fff',
        hoverBgColor: '#F2F2F2'
    }
}
export default {
    name: 'SketchRuler',
    components: {
        RulerWrapper
    },
    data() {
        return {
            vertical: true,
        }
    },
    props: {
        scale: {
            type: Number,
            default: 1,
        },
        ratio: {
            type: Number,
            default: window.devicePixelRatio || 1,
        },
        thick: {
            type: Number,
            default: 16,
        },
        width: Number,
        height: Number,
        startX: {
            type: Number,
            default: 0,
        },
        startY: {
            type: Number,
            default: 0,
        },
        shadow: {
            type: Object,
            default: () => {
                return {
                    x: 200,
                    y: 100,
                    width: 200,
                    height: 400
                };
            },
        },
        horLineArr: {
            type: Array,
            default: () => {
                return [100, 200];
            },
        },
        verLineArr: {
            type: Array,
            default: () => {
                return [100, 200];
            },
        },
        cornerActive: Boolean,
        lang: String,
        isOpenMenuFeature: false,
        handleShowRuler: {
            type: Function,
            default: () => {
                return () => {};
            },
        },
        isShowReferLine: {
            type: Boolean,
            default: true,
        },
        handleShowReferLine: {
            type: Function,
            default: () => {
                return () => {};
            },
        },
        palette: {
            type: Object,
            default: () => {
                return {
                    bgColor: 'rgba(225,225,225, 0)', // ruler bg color
                    longfgColor: '#BABBBC', // ruler longer mark color
                    shortfgColor: '#C8CDD0', // ruler shorter mark color
                    fontColor: '#7D8694', // ruler font color
                    shadowColor: '#E8E8E8', // ruler shadow color
                    lineColor: '#EB5648',
                    borderColor: '#DADADC',
                    cornerActiveColor: 'rgb(235, 86, 72, 0.6)',
                    menu: DEFAULTMENU
                }
            },
        }
    },
    computed: {
        cornerActiveClass() {
            return this.cornerActive ? ' active' : '';
        },
        cornerStyle() {
            return {
                backgroundColor: this.palette.bgColor,
                width: this.thick + 'px',
                height: this.thick + 'px',
                borderRight: `1px solid ${this.palette.borderColor}`,
                borderBottom: `1px solid ${this.palette.borderColor}`,
            }
        },
        canvasConfigs() {
            const {
                bgColor,
                longfgColor,
                shortfgColor,
                fontColor,
                shadowColor,
                lineColor,
                borderColor,
                cornerActiveColor
            } = this.palette;
            return {
                ratio: this.ratio,
                bgColor,
                longfgColor,
                shortfgColor,
                fontColor,
                shadowColor,
                lineColor,
                borderColor,
                cornerActiveColor
            }
        }
    },
    methods: {
        onCornerClick(e) {
            this.$emit('onCornerClick', e);
        },
        handleLineChange(arr, vertical) {
            const newLines = vertical
            ? { h: this.horLineArr, v: [...arr] }
            : { h: [...arr], v: this.verLineArr }
            this.$emit('handleLine', newLines);
        }
    }
}
</script>

<style lang="less">
.style-ruler {
    position: absolute;
    width: 100%; /* scrollbar width */
    height: 100%;
    z-index: 3; /* 需要比resizer高 */
    pointer-events: none;
    font-size: 12px;
    overflow: hidden;
    span {
        line-height: 1;
    }
}
.corner {
    position: absolute;
    left: 0;
    top: 0;
    pointer-events: auto;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
    box-sizing: content-box;
    // &.active {
    //     background-color: ${props => props.cornerActiveColor} !important;
    // }
}

.indicator {
    position: absolute;
    pointer-events: none;
    .value {
        position: absolute;
        background: white;
    }
}
.corner {
    position: absolute;
    left: 0;
    top: 0;
    
    pointer-events: auto;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
    box-sizing: content-box;
    &.active {
        // background-color: ${props => props.cornerActiveColor} !important;
    }
}
.ruler {
    width: 100%;
    height: 100%;
    pointer-events: auto;
}
</style>