<p><a target="_blank" rel="noopener noreferrer" href="https://camo.githubusercontent.com/95db0da88a729ba45efa1a2ed71350eb69896c4e/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f762f76322d646174657069636b65722e737667"><img src="https://camo.githubusercontent.com/95db0da88a729ba45efa1a2ed71350eb69896c4e/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f762f76322d646174657069636b65722e737667" alt="npm-version" data-canonical-src="https://img.shields.io/npm/v/v2-datepicker.svg" style="max-width:100%;"></a> <a target="_blank" rel="noopener noreferrer" href="https://camo.githubusercontent.com/28479a7a834310a667f36760a27283f7389e864a/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f6c2f76322d646174657069636b65722e737667"><img src="https://camo.githubusercontent.com/28479a7a834310a667f36760a27283f7389e864a/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f6c2f76322d646174657069636b65722e737667" alt="license" data-canonical-src="https://img.shields.io/npm/l/v2-datepicker.svg" style="max-width:100%;"></a></p>

<p>English | <a href="https://github.com/chuxiaoguo/vue-sketch-ruler/blob/master/README.zh-CN.md">简体中文</a></p>

## vue-sketch-ruler

> A sketch like ruler in vue

## Live Demo
[click here](https://chuxiaoguo.github.io/vue-sketch-ruler/)

## Install
```
npm install --save vue-sketch-ruler
```
## Supported features
- [x] ruler render
- [x] ruler render when scale
- [x] ruler render when srolling
- [x] switch status of ruler(show or hide)
- [x] reference line management
- [x] switch status of reference line (show or hide)

## Upcoming features

- [] contextmenu of ruler
- [] add event on corner
- [] separate css style
- [] international

## Usage
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
A complete example can be found [here](https://github.com/chuxiaoguo/vue-sketch-ruler/blob/master/docs/src/components/UserRuler.vue)

## api
### Interface <TypeScript>
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
### Attributes
|  Attributes|  Description | Type | Default |
| --- | --- | --- | --- |
| lang | init language lang | String | zh-CN |
| scale | ruler scale size | Number | 2 |
| thick | thick size | Number | 16 |
| width | the window width of the currently loaded ruler  | Number | - |
| height | the window height of the currently loaded ruler  | Number | - |
| startX | x at the beginning of the ruler | Number | 0 |
| startY | y at the beginning of the ruler | Number | 0 |
| shadow |  size and the start coordinates on the ruler of the shadow  | Shadow | 0 |
| startY | y at the beginning of the ruler | Number | {x: 200,y: 100,width: 200,height: 400} |
| horLineArr | Initial values for horizontal reference lines | Array<number> | [] |
| verLineArr | Initial values for vertical reference lines  | Array<number> | [] |
| palette | the palette of sketch ruler | Palette | {bgColor: 'rgba(225,225,225, 0)',longfgColor: '#BABBBC',shortfgColor: '#C8CDD0',fontColor: '#7D8694', shadowColor: '#E8E8E8',lineColor: '#EB5648', borderColor: '#DADADC',cornerActiveColor: 'rgb(235, 86, 72, 0.6)',} |


### Event

| EventName | Description | CallbackParam |
| --- | --- | --- |
| handleLine | horizontal or vertical reference lines has changed (add or remove) | Lines  |

## License
MIT

## reference
a react component [mb-sketch-ruler](https://github.com/mockingbot/mb-sketch-ruler) from mockingbot.
