<template>
<h1>{{ msg }}</h1>
<button @click="state.count++">count is: {{ state.count }}</button>
<button @click="stop">stop count</button>

<p>
    Edit <code>components/HelloWorld.vue</code> to test hot module replacement.
</p>
<p>double count : {{ state.double }}</p>
<div ref="root">{{x}} - {{y}}</div>
<Child :name="state.name" @showChildData="showChildData">
    <p>slot插槽测试 {{state.double}}</p>
    <template v-slot:footer>
        <p>具名插槽测试 {{state.double}}</p>
    </template>

</Child>
</template>

<script>
import Child from './Child.vue'
import {
    reactive,
    computed,
    watchEffect,
    onMounted,
    ref,
    onUnmounted,
    provide
} from "vue";

function useMousePosition() {
    const x = ref(0)
    const y = ref(0)

    function update(e) {
        x.value = e.pageX
        y.value = e.pageY
    }

    onMounted(() => {
        window.addEventListener('mousemove', update)
    })

    onUnmounted(() => {
        window.removeEventListener('mousemove', update)
    })

    return {
        x,
        y
    }
}

export default {
    name: "HelloWorld",
    props: {
        msg: String,
    },
    components: {
        Child
    },
    // data() {
    //     return {
    //         count: 0,
    //     }
    // },
    setup(props) {
        const root = ref(null)
        const themeRef = ref('dark')
        const {
            x,
            y
        } = useMousePosition()
        const state = reactive({
            count: 0,
            double: computed(() => state.count * 2),
            id: '',
            name: 'zjh'
        });

        // watchEffect(() => {
        //     console.log(state.double)
        // })

        onMounted(() => {
            console.log(this + 'xxxxxxxxxxxxx')
            console.log(root.value)
            state.id = setInterval(() => {
                state.count++;
            }, 1000);
            console.log(state.id);
        })

        const showChildData = (childValue) => {
            console.log(childValue)
        }

        // method
        const stop = () => {
            clearInterval(state.id)
            console.log("stop count ok")
        }
        return {
            state,
            stop,
            x,
            y,
            showChildData,
            root
        };

    },
    // mounted() {
    //     this.id = setInterval(() => {
    //         this.state.count++;
    //     }, 1000);
    //     console.log(this.id);
    // },
};
</script>
