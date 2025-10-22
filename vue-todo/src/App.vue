<script setup lang="ts">
import { reactive, computed } from 'vue';
import TodoForm from './components/TodoForm.vue';
import TodoList from './components/TodoList.vue';

interface Todo {
  id: number
  text: string
  done: boolean
}

// Array almacenar lista de tareas
const todos = reactive<Todo[]>([]);

function addTodo(text: string) {
  todos.push({ id: Date.now(), text, done: false })
};
//Cammbiar el estado de una tarea
function toggleTodo(id: number) {
  const todo = todos.find(t => t.id === id)
  if (todo) todo.done = !todo.done
};

function removeTodo(id: number) {
  const index = todos.findIndex(t => t.id === id)
  if (index !== -1) todos.splice(index, 1)
};

const totalDone = computed(()=> tasks
  .value
  .reduce((total,task)=> task.done ? total+1: total, 0 ));
// Contador tareas
const remaining = computed(() => todos.filter(t => !t.done).length);
</script>

<template>
  <div class="app">
    <h1>Mi To-Do List</h1>
    <TodoForm @add-todo="addTodo" />
    <p v-if="todos.length === 0">No hay tareas aún</p>

    <transition-group name="fade" tag="ul">
      <TodoList
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle-todo="toggleTodo"
        @remove-todo="removeTodo"
      />
    </transition-group>

    <p class="remaining">Tareas pendientes: {{ remaining }}</p>
  </div>
</template>

<style scoped>
  .app {
    max-width: 500px;
    margin: 2rem auto;
    padding: 1.5rem;
    border-radius: 16px;
    background: #eef;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
  h1 {
    text-align: center;
    color: #333;
  }
  li{
    color:#000f;
  }
  .remaining {
    text-align: center;
    margin-top: 1rem;
    font-weight: 600;
  }
  .fade-enter-active, .fade-leave-active {
    transition: all 0.3s ease;
  }
  .fade-enter-from, .fade-leave-to {
    opacity: 0;
    transform: translateY(10px);
  }
</style>
