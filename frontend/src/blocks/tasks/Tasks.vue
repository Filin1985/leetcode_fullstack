<template>
  <section class="tasks">
    <div class="tasks__header">
      <h2 class="tasks__title">Задачи</h2>
      <div class="tasks__filters">
        <h4 class="tasks__filters-title">Фильтры</h4>
        <div class="tasks__categories">
          <p
            class="tasks__category"
            :class="{tasks__category_active: activeFilter === 'all'}"
            @click="setFilter('all')"
          >
            All categories ({{ totalProblems }})
          </p>
          <p
            class="tasks__category"
            v-for="(count, category) in categories"
            :key="category"
            :class="{tasks__category_active: activeFilter === category}"
            @click="setFilter(category)"
          >
            {{ category }} ({{ count }})
          </p>
        </div>
      </div>
    </div>
    <ul class="tasks__items">
      <Task
        v-for="problem in filteredProblems"
        :key="problem.id"
        :title="problem.title"
        :description="problem.description"
        :difficulty="problem.difficulty"
        :createdAt="problem.createdAt"
        :updatedAt="problem.updatedAt"
        :timesSolved="problem.timesSolved"
        :category="problem.category"
      />
    </ul>
  </section>
</template>

<script setup lang="ts">
import {computed, onMounted, ref} from "vue"
import Task from "../../components/task/Task.vue"

interface ProblemAttributes {
  id?: number
  title: string
  description: string
  difficulty: "easy" | "medium" | "hard"
  testCases: object
  constraints: string
  examples: object
  timesSolved: number
  category: string
  hints?: string
  isActive?: boolean
  createdAt?: Date
  updatedAt?: Date
}

const problems = ref<ProblemAttributes[]>([])
const activeFilter = ref<string>("all")

onMounted(async () => {
  try {
    const response = await fetch("http://localhost:3000/api/problems")
    const data = await response.json()
    problems.value = data.data
  } catch (error) {
    console.error("Error fetching problems:", error)
  }
})

const categories = computed(() => {
  return problems.value.reduce((acc: Record<string, number>, problem) => {
    acc[problem.category] = (acc[problem.category] || 0) + 1
    return acc
  }, {})
})

const filteredProblems = computed(() => {
  return problems.value.filter((problem) => {
    const matchesCategory =
      activeFilter.value === "all" || problem.category === activeFilter.value
    return matchesCategory
  })
})

const totalProblems = computed(() => problems.value.length)

const setFilter = (category: string) => {
  activeFilter.value = category
}
</script>

<style lang="scss" scoped>
.tasks__items {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 10px;
  margin: 0;
}

.tasks__header {
  display: flex;
  flex-direction: column;
}

.tasks__categories {
  display: flex;
  gap: 20px;
}

.tasks__category {
  padding: 8px 16px;
  background-color: #e5e7eb;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin: 0;
  color: black;

  &:hover {
    background-color: #d1d5db;
  }

  &_active {
    background-color: #3b82f6;
    color: white;
  }
}
</style>
