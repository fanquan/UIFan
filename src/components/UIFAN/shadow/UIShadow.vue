<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

@Component
export default class UIShadow extends Vue {
    @Prop([String, Number]) readonly shadow: string | number | undefined;

    protected get ShadowValue() {
        if (this.shadow) return `ui-shadow--${this.shadow}`;

        return "ui-shadow--0";
    }
}
</script>

<style lang="stylus">
Shadow(a, b, c)
    box-shadow 0 a rgba(0,0,0,0.2), 0 b rgba(0,0,0,0.14), 0 c rgba(0,0,0,0.12)
&.ui-shadow--1
    Shadow(2px 1px -1px, 1px 1px 0, 1px 3px 0)
&.ui-shadow--2
    Shadow(3px 1px -2px, 2px 2px 0, 1px 5px 0)
&.ui-shadow--3
    Shadow(3px 3px -2px, 3px 4px 0, 1px 8px 0)
&.ui-shadow--4
    Shadow(2px 4px -1px, 4px 5px 0, 1px 10px 0)
&.ui-shadow--5
    Shadow(3px 5px -1px, 5px 8px 0, 1px 14px 0)
&.ui-shadow--6
    Shadow(3px 5px -1px, 6px 10px 0, 1px 18px 0)
&.ui-shadow--7
    Shadow(4px 5px -2px, 7px 10px 1px, 2px 16px 1px)
&.ui-shadow--8
    Shadow(5px 5px -3px, 8px 11px 1px, 3px 14px 2px)
&.ui-shadow--9
    Shadow(5px 6px -3px, 9px 12px 1px, 3px 16px 2px)
&.ui-shadow--10
    Shadow(6px 6px -3px, 10px 14px 1px, 4px 18px 3px)
</style>
