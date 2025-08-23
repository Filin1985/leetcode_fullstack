<template>
    <div class="task">
        <div class="task__header">
            <h3 class="task__title">{{ title }}</h3>
            <div class="task__info">
                <p>Popularity - <span class="task__solved">{{ timesSolved }}</span> times solved</p>
                <p class="task__category">{{ category }}</p>
            </div>
        </div>

        <div class="task__description">
            <p class="task__text">{{ description }}</p>
            <Tag :text="difficulty" />
        </div>
        <div class="task__date">
            <p class="task__created">Created - {{ createdAt }}</p>
            <p class="task__updated">Updated - {{ updatedAt }}</p>
        </div>
    </div>
</template>

<script setup lang="ts">
import Tag from '../../ui/tag/Tag.vue';

const props = defineProps(["title", "description", "difficulty", "timesSolved", "category", "createdAt", "updatedAt"]);

</script>

<style lang="scss" scoped>
    .task {
    border: 1px solid goldenrod;
    border-radius: 10px;
    padding: 15px;

    &__header {
        display: flex;
        justify-content: space-between;
    }

    &__info {
        display: flex;
        gap: 20px;
    }

    &__category {
        padding: 0 5px;
        border-radius: 5px;
        background-color: lightgray;
        color: black;
    }

    &__solved {
        font-weight: bold;
    }

    &__title {
        display: flex;
        flex-direction: column;
        margin: 0;
    }

    &__description {
        display: flex;
        justify-content: space-between;
        gap: 50px;

        p {
            margin: 10px 0;
        }
    }

    &__date {
        display: flex;
        justify-content: space-between;

        p {
            margin: 10px 0;
        }
    }
}

.task:hover {
    cursor: pointer;
    border: 1px solid green;
}
</style>