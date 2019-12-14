<p><a target="_blank" rel="noopener noreferrer" href="https://camo.githubusercontent.com/95db0da88a729ba45efa1a2ed71350eb69896c4e/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f762f76322d646174657069636b65722e737667"><img src="https://camo.githubusercontent.com/95db0da88a729ba45efa1a2ed71350eb69896c4e/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f762f76322d646174657069636b65722e737667" alt="npm-version" data-canonical-src="https://img.shields.io/npm/v/v2-datepicker.svg" style="max-width:100%;"></a> <a target="_blank" rel="noopener noreferrer" href="https://camo.githubusercontent.com/28479a7a834310a667f36760a27283f7389e864a/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f6c2f76322d646174657069636b65722e737667"><img src="https://camo.githubusercontent.com/28479a7a834310a667f36760a27283f7389e864a/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f6c2f76322d646174657069636b65722e737667" alt="license" data-canonical-src="https://img.shields.io/npm/l/v2-datepicker.svg" style="max-width:100%;"></a></p>

<p>English<a href="https://github.com/chuxiaoguo/vue-sketch-ruler"> | 简体中文</a></p>

## vue-sketch-ruler

> 一个vue组件的素描标尺

## 在线demo
[点击这里查看](https://chuxiaoguo.github.io/vue-sketch-ruler/)

## 安装
> 支持全局导入和模块导入
```
npm install --save vue-sketch-ruler
```
## 支持的功能
- [x] 标尺渲染
- [x] 缩放内容，重绘标尺
- [x] 滚动内容，重绘标尺
- [x] 切换标尺状态，显示或隐藏
- [x] 参考线管理（增加删除）
- [x] 切换参考线状态，显示或隐藏

## 未来支持的功能

- [] 支持标尺的右键菜单
- [] 标角支持事件
- [] 分离css样式，支持导入样式
- [] 国际化

## 使用
```
<template>
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
            lang: "zh-CN",
            isShowRuler: true,
            isShowReferLine: true
        }
    },
    components: {
        SketchRule
    }
});
</script>
```
参考一个完整的例子，[点击这里](https://github.com/chuxiaoguo/vue-sketch-ruler/blob/master/docs/src/components/UserRuler.vue)

## api
### 接口 <TypeScript>
```
interface Lines {
    h: number[],
    v:  Array<Number>,
}
interface Shadow {
    x: number,
    y: number,
    width: number,
    height: number
}
interface Palette {
    bgColor: string, // ruler bg color
    longfgColor: string, // ruler longer mark color
    shortfgColor: string, // ruler shorter mark color
    fontColor: string, // ruler font color
    shadowColor: string, // ruler shadow color
    lineColor: string,
    borderColor: string',
    cornerActiveColor: string,
}
```
### 属性

|  属性名称|  描述 | 类型 | 默认值 |
| --- | --- | --- | --- |
| lang | 初始化的语言 | String | zh-CN |
| scale | 初始化标尺的缩放 | Number | 2 |
| thick | 标尺的厚度 | Number | 16 |
| width | 放置标尺窗口的宽度  | Number | - |
| height | 放置标尺窗口的高度  | Number | - |
| startX | x轴标尺开始的坐标数值 | Number | 0 |
| startY | y轴标尺开始的坐标数值 | Number | 0 |
| shadow |  阴影的参数  | Shadow | 0 |
| horLineArr | 初始化水平标尺上的参考线 | Array<number> | [] |
| verLineArr | 初始化垂直标尺上的参考线  | Array<number> | [] |
| palette | 标尺的样式配置参数 | Palette | {bgColor: 'rgba(225,225,225, 0)',longfgColor: '#BABBBC',shortfgColor: '#C8CDD0',fontColor: '#7D8694', shadowColor: '#E8E8E8',lineColor: '#EB5648', borderColor: '#DADADC',cornerActiveColor: 'rgb(235, 86, 72, 0.6)',} |


### Event

| 事件名称 | 描述 | 回调参数 |
| --- | --- | --- |
| handleLine | 在横纵标尺上操作参考线（新增或移除） | Lines  |

## 引用
一个来自墨刀的react标尺组件 [mb-sketch-ruler](https://github.com/mockingbot/mb-sketch-ruler) .
