<template>
    <aside class="sidebar">
        Sidebar
        <Button text="Click me!!!" @click="count++"/>
        <p>{{count}}</p>
    </aside>
</template>

<script setup lang="ts">
import { onBeforeUnmount, onBeforeUpdate, onMounted, onUpdated, ref } from 'vue';
import Button from '../../ui/button/Button.vue';

const count = ref(0)

onBeforeUpdate(() => {
    console.log(count)
})

onUpdated(() => {
    console.log(count)
})

</script>

<style lang="scss" scoped>
.sidebar {
    height: 100%;
    width: 20%;
    background-color: #272a2d;
}
</style>