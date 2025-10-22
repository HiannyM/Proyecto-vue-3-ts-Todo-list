<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'

interface Todo {
    id: number
    text: string
    done: boolean
}

const props = defineProps<{ todo: Todo }>()
const emit = defineEmits(['toggle-todo', 'remove-todo'])
</script>

<template>
    <li 
        class="todo-item" 
        :class="{ done: props.todo.done }"
        
    >
        <span @click="emit('toggle-todo', props.todo.id)">
        {{ props.todo.text }}
        </span>
        <button @click="emit('remove-todo', props.todo.id)">❌</button>
    </li>
</template>

<style scoped>

    .todo-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: #fafafa;
        margin-bottom: 0.4rem;
        padding: 0.5rem 0.8rem;
        border-radius: 8px;
        border: 1px solid #eee;
        cursor: pointer;
    }
    .todo-item.done span {
        text-decoration: line-through;
        color: #999;
    }
    .todo-item button {
        background: transparent;
        border: none;
        cursor: pointer;
    }
</style>
