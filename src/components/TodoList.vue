<template>
  <v-container>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @check-todo="checkTodo"
      @delete-todo="deleteTodo"
    />

    <AddTodoButton @add-todo="addTodo" />
  </v-container>
</template>

<script setup>
  import { ref, watch, onMounted } from 'vue';
  import TodoItem from './TodoItem.vue';
  import AddTodoButton from './AddTodoButton.vue';

  const todos = ref([]);

  // Récupère les données du localStorage au chargement de la page
  onMounted(() => {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      todos.value = JSON.parse(savedTodos);
    }
  });

  // Sauvegarde les données dans le localStorage à chaque modification
  watch(todos, (newTodos) => {
    localStorage.setItem('todos', JSON.stringify(newTodos));
  }, { deep: true });

  const addTodo = () => {
    const newTodo = {
      id: Date.now(),
      text: "Nouvelle tâche",
      completed: false,
    };
    todos.value.push(newTodo);
  };

  const checkTodo = (id) => {
    const todo = todos.value.find(t => t.id === id);
    if (todo) {
      todo.completed = !todo.completed;
    }
  };

  const deleteTodo = (id) => {
    todos.value = todos.value.filter(t => t.id !== id);
  };
</script>