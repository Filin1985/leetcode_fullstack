<template>
    <div>
        <h2>Задачи</h2>
        <div>
            <p>All categories</p>
            <p v-for="(count, category) in categories">
                {{ category }} {{ count }}
            </p>
        </div>
        <p>Фильтры</p>
    </div>
    <h2>Задачи</h2>
    <ul class="tasks">
        <Task v-for="problem in problems" :title="problem.title" :description="problem.description"
            :difficulty="problem.difficulty" :createdAt="problem.createdAt" :updatedAt="problem.updatedAt"
            :timesSolved="problem.timesSolved" :category="problem.category" />
    </ul>
</template>

<script setup lang="ts">
import {computed, onMounted, ref} from "vue";
import Task from "../../components/task/Task.vue";

interface ProblemAttributes {
    id?: number;
    title: string;
    description: string;
    difficulty: 'easy' | 'medium' | 'hard';
    testCases: object;
    constraints: string;
    examples: object;
    timesSolved: number;
    category: string;
    hints?: string;
    isActive?: boolean;
    createdAt?: Date;
    updatedAt?: Date;
}

const problems = ref<ProblemAttributes[]>([]);

onMounted(async () => {
    try {
        const response = await fetch("http://localhost:3000/api/problems");
        const data = await response.json();
        problems.value = data.data;
        console.log(data);
        console.log("Computed categories:", categories.value);
    } catch (error) {
        console.log(error);
    }
});

const categories = computed(() => {
    return problems.value.reduce((acc: Record<string, number>, problem) => {
        acc[problem.category] = (acc[problem.category] || 0) + 1;
        return acc;
    }, {});
});

</script>

<style lang="scss" scoped>
.tasks {
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 10px;
    margin: 0;
}
</style>