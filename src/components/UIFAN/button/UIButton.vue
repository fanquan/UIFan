<template>
    <button
        @click="onClickBtn"
        :class="[
            'ui-btn',
            ShadowValue,
            size ? `ui-btn--${size}` : '',
            border === 'dashed'
                ? 'ui-btn--dashed'
                : border
                ? 'ui-btn--solid'
                : '',
            {
                'ui-btn--round': round,
                'ui-btn--square': square,
                'ui-btn--circle': circle,
                'ui-btn--disabled': disabled,
                'ui-btn--loading': loading,
                'ui-btn--text': text,
                'ui-btn--icon': icon,
            },
        ]"
        :style="
            `
            --color-tint: ${TintColor};
            --color-title: ${TitleColor}
        `
        "
    >
        <div v-if="loading" class="ui-loading-circle ui-icon--default ">
            <img src="../../../assets/icons/loading.gif" alt="" />
        </div>
        <div v-if="icon" class="ui-icon--default">
            <img :src="icon" alt="" />
        </div>
        <span v-if="$slots.default"><slot>按钮</slot></span>
        <slot v-else>按钮</slot>
    </button>
</template>

<script lang="ts">
import { Component, Vue, Emit, Prop, Mixins } from "vue-property-decorator";
import UIShadow from "../shadow/UIShadow.vue"

@Component
export default class UIButton extends Mixins(UIShadow) {
    // 尺寸 mini small normal large
    @Prop(String) readonly size: string | undefined;

    //形状
    @Prop(Boolean) readonly round: boolean | undefined; //圆角
    @Prop(Boolean) readonly square: boolean | undefined; //方形
    @Prop(Boolean) readonly circle: boolean | undefined; //圆形

    // 禁用
    @Prop(Boolean) readonly disabled: boolean | undefined;

    // 颜色
    @Prop(String) readonly color: string | undefined; //颜色
    @Prop(String) readonly titleColor: string | undefined; //颜色

    // 按钮类型
    @Prop(Boolean) readonly text: boolean | undefined; //文本按钮
    @Prop([Boolean, String]) readonly border: boolean | string | undefined; // 边框按钮
    @Prop(Boolean) readonly loading: string | undefined; // 加载中按钮
    @Prop(String) readonly icon: string | undefined; // 图标按钮

    @Prop([String, Number]) readonly shadow: string | number | undefined;

    @Emit("click") private emitClick(event: MouseEvent) {}

    // 计算属性
    private get TintColor() {
        if (this.color) {
            return this.color;
        }
        return "#2d8cf0";
    }

    private get TitleColor() {
        if (this.titleColor) {
            return this.titleColor;
        }
        if (this.border || this.text) {
            console.log("---", this.text);
            return this.color;
        }
        return "#17233d";
    }

    private onClickBtn(event: MouseEvent) {
        if (!this.disabled) {
            this.emitClick(event);
        }
    }
}
</script>

<style lang="stylus" scoped>
@import "../style/var.styl";

resize(minWidth, height, paddingLR, fontSize)
    min-width minWidth
    height height
    padding 0 paddingLR
    font-size fontSize
    &.ui-btn--round, &.ui-btn--circle
        border-radius (@height / 2)
    &.ui-btn--circle
        width @height
        min-width 0
        padding 0
    .ui-icon--default
        font-size (@font-size + 2)
.ui-btn
    min-width 64px
    resize($button-normal-width, $button-normal-height, $button-normal-paddingLR,$button-normal-font-size)
    border 0 solid black
    border-radius 4px
    font-weight 500
    letter-spacing 0.09em
    cursor pointer
    color var(--color-title, #17233d)
    background-color var(--color-tint, #2d8cf0)
    outline none
    user-select none
    box-sizing border-box
    -webkit-tap-highlight-color: transparent;
    &:focus
        outline none
    &:hover
        filter brightness(110%)
    &:active
        filter brightness(90%)

    &.ui-btn--mini
        resize($button-mini-width, $button-mini-height, $button-mini-paddingLR,$button-mini-font-size)
    &.ui-btn--small
        resize($button-small-width, $button-small-height, $button-small-paddingLR,$button-small-font-size)
    &.ui-btn--large
        resize($button-large-width, $button-large-height, $button-large-paddingLR,$button-large-font-size)
    &.ui-btn--normal
        resize($button-normal-width, $button-normal-height, $button-normal-paddingLR,$button-normal-font-size)
    &.ui-btn--long
        width 100%
        height 50px
    &.ui-btn--square
        border-radius 0
    &.ui-btn--disabled
        background-color #efeff6
        color #bbbdc1
        cursor not-allowed
    &.ui-btn--loading, &.ui-btn--icon
        position relative
        vertical-align middle
        .ui-icon--default
                display inline-block
                margin-right 4px
                line-height 0
                >img
                    vertical-align: middle
                    width 1em
                    height 1em
                    display inline-block
    &.ui-btn--solid
        border 1px solid var(--color-title, #17233d)
    &.ui-btn--dashed
        border 1px dashed var(--color-title, #17233d)
    &.ui-btn--text,&.ui-btn--solid, &.ui-btn--dashed
        background-color transparent
</style>
