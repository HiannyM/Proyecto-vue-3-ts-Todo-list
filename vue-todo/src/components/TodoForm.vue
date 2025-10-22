<script setup lang="ts">
    import { ref } from 'vue';

    const emit = defineEmits(['add-todo']);
    const text = ref('');

    function onSubmit() {
        if (!text.value.trim()) return alert('Escribe una tarea')
        emit('add-todo', text.value.trim())
        text.value = ''
    }
</script>

<template>
    <form 
        class="todo-form" 
        @submit.prevent="onSubmit"
    >
            <input 
                v-model="text"
                placeholder="Nueva tarea..." 
            />
            <button type="submit">Agregar</button>
    </form>
</template>

<style scoped>
    .todo-form {
        display: flex;
        gap: 0.5rem;
        margin-bottom: 1rem;
    }
    input {
        flex: 1;
        padding: 0.6rem;
        border-radius: 8px;
        border: 1px solid #ccc;
    }
    button {
        padding: 0.6rem 1rem;
        border: none;
        border-radius: 8px;
        background: #42b883;
        color: white;
        cursor: pointer;
        transition: 0.2s;
    }
    button:hover {
        background: #2f9e73;
    }
</style>
