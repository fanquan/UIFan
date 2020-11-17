<template>
    <div>
        <div class="btn-demo">
            <UIButton
                @click="onClick"
                :size="size"
                :square="square"
                :round="round"
                :circle="circle"
                color="orange"
            ></UIButton>
        </div>
        <div class="section">
            <h2>按钮尺寸</h2>
            <p>支持 large 、normal 、small 、mini</p>
            <div class="demo-size">
                <UIButton @click="resize('mini')">超小</UIButton>
                <UIButton @click="resize('small')">小</UIButton>
                <UIButton @click="resize('normal')">正常</UIButton>
                <UIButton @click="resize('large')">大</UIButton>
            </div>
        </div>

        <div class="section">
            <h2>按钮形状</h2>
            <p>
                通过 square 设置方形按钮，通过 round 设置圆角按钮，
                circle设置圆形按钮。
            </p>
            <div class="demo-size">
                <UIButton square="square">矩形按钮</UIButton>
                <UIButton>正常按钮</UIButton>
                <UIButton round="round">圆角按钮</UIButton>
                <UIButton circle="circle">圆形</UIButton>
            </div>
        </div>
        <div class="section">
            <h2>按钮禁用</h2>
            <p>
                通过 disabled 设置按钮禁用
            </p>
            <div class="demo-size">
                <UIButton @click="changeDisable(false)">启用</UIButton>
                <UIButton @click="changeDisable(true)" :disabled="disabled"
                    >禁用</UIButton
                >
            </div>
        </div>

        <div class="section">
            <h2>设置按钮颜色</h2>
            <p>
                通过 color 设置按钮颜色
            </p>
            <div class="demo-size">
                <UIButton>默认</UIButton>
                <UIButton color="orange">橘色</UIButton>
                <UIButton color="#fe4444">红色</UIButton>
                <UIButton color="#7f69ff">紫色</UIButton>
                <UIButton color="#7f69ff" :shadow="3">紫色</UIButton>

               
            </div>
        </div>

        <div class="section">
            <h2>设置按钮阴影</h2>
            <p>通过shadow设置</p>
             <div class="demo-size">
                <UIButton size="small">无阴影</UIButton>
                <UIButton :shadow="5" size="small" color="#fe4444">阴影5</UIButton>
                <UIButton shadow="10" size="small" color="#7f69ff">阴影10</UIButton>
            </div>
        
        </div>

        <div class="section">
            <h2>设置按钮类型</h2>
            <p>
                通过 loading 、icon、 text、border 设置按钮类型
            </p>
            <div class="demo-size">
                <UIButton loading size="small">加载中</UIButton>
                <UIButton :icon="require('./assets/logo.png')" size="small">图标</UIButton>
                <UIButton text size="small" color="#fe4444">文本</UIButton>
                <UIButton border size="small" color="#fe4444">实现边框</UIButton>
                <UIButton border="dashed" size="small" color="#7f69ff">虚线边框</UIButton>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import UIButton from "./components/UIFAN/button/UIButton.vue";
import { Component, Vue } from "vue-property-decorator";

@Component({
    components: {
        UIButton,
    },
})

// 继承子Vue才是一个vue组件
export default class App extends Vue {
    private size: string = "mini";
    private square: boolean = false;
    private round: boolean = false;
    private circle: boolean = false;
    private disabled: boolean = false;

    private resize(name: string) {
        this.size = name;
    }

    private changeRadius(name: string) {
        switch (name) {
            case "square":
                this.square = true;
                this.round = false;
                this.circle = false;
                break;
            case "round":
                this.round = true;
                this.square = false;
                this.circle = false;
                break;
            case "circle":
                this.circle = true;
                this.square = false;
                this.round = false;
                break;
            case "normal":
                this.square = false;
                this.round = false;
                this.circle = false;
        }
    }

    private changeDisable(flag: boolean) {
        this.disabled = flag;
    }
    private onClick(event: MouseEvent) {
        console.log("btn click", event);
    }
}
</script>

<style lang="stylus" scoped>
.btn-demo
    display flex
    justify-content center
.demo-size
    margin-top 20px
    button
        margin-right 20px
.section
    >p
        color #666
</style>
