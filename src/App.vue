<template>
<div id="app">
    <home></home>
</div>
</template>

<script lang="ts">
// 引入组件、装饰器
import {
    Component,
    Vue
} from "vue-property-decorator";
import Home from "@/Home.vue";

// 装饰器：表示将这个装饰器当做一个类来使用
@Component({
    components: {
        Home,
    },
})

// 继承子Vue才是一个vue组件
export default class App extends Vue {}
</script>

<style lang="stylus"></style>
