<template>
    <div class="tag">
        <p class="difficulty">{{ text }}</p>
    </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
const props = defineProps(["text", "color"]);

const tagColor = computed(() => {
    switch (props.text.toLowerCase()) {
        case "easy":
            return "green";
        case "medium":
            return "orange";
        case "hard":
            return "red";
        default:
            return props.color || "gray";
    }
});

</script>

<style lang="scss" scoped>
p {
    margin: 10px 0;
    background-color: v-bind(tagColor);
    padding: 5px 10px;
    border-radius: 10px;
    border: 0.5px solid tan
}
</style>