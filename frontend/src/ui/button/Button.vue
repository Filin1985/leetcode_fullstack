<template>
    <button class="button">
        {{props.text}}
    </button>
</template>

<script setup lang="ts" >
import { reactive, toRefs } from 'vue'

const props = defineProps(['text'])

</script>

<style lang="scss" scoped>

</style>