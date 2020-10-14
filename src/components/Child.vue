<template>
<h1>i'm children component, test provide/inject</h1>
<p>inject {{ color }}</p>
<p>props {{ color }}</p>
<div v-for="(item, i) in list" :ref="el => { divs[i] = el }" :key="i">
    {{ item }} -- {{ i }}
</div>
<button @click="childClick">click me</button>
<slot></slot>
<slot name="footer"></slot>
</template>

<script>
import {
    inject,
    reactive,
    onBeforeUpdate,
    onUpdated
} from "vue";

export default {
    name: "Child",
    props: {
        name: String,
    },
    emits: {
        showChildData: (payload) => {
            return payload;
        },
    },
    setup(props, content) {
        const list = reactive([1, 2, 3]);
        const divs = reactive([]);

        const color = inject("ThemeSymbol");

        const childClick = () => {
            // 需要申请emits，不然会一直提示警告。
            content.emit("showChildData", "test");
        };

        onBeforeUpdate(() => {
            divs.value = []
        })
        onUpdated(() => {
            console.log(divs)
        })
        return {
            color,
            childClick,
            list,
            divs,
        };
    },
};
</script>
