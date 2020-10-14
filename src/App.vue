<template>
<img alt="Vue logo" src="./assets/logo.png" />
<HelloWorld :msg="msg" />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
    name: 'App',
    components: {
        HelloWorld
    },
    data() {
        return {
            msg: 'first time use this !'
        }
    }
}
</script>
