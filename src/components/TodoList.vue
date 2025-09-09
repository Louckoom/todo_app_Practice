<template>
  <div class="px-3">
    <div v-for="todo in todos" :key="todo.id">
      <TodoItem 
        :todo="todo"
        @check-todo="emit('check-todo', $event)"
        @delete-todo="emit('delete-todo', $event)"
        @add-sub-todo="emit('add-sub-todo', $event)"
      />
      <div v-if="todo.subTodos && todo.subTodos.length > 0" class="pl-6">
        <TodoList 
          :todos="todo.subTodos" 
          @check-todo="emit('check-todo', $event)"
          @delete-todo="emit('delete-todo', $event)"
          @add-sub-todo="emit('add-sub-todo', $event)"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
  import { defineProps, defineEmits } from 'vue';
  import TodoItem from './TodoItem.vue';

  const props = defineProps({
    todos: {
      type: Array,
      required: true
    }
  });

  const emit = defineEmits(['check-todo', 'delete-todo', 'add-sub-todo']);
</script>