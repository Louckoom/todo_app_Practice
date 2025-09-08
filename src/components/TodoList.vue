<template>
  <v-container>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
    />

    <AddTodoButton @add-todo="addTodo" />
  </v-container>
</template>

<script setup>
  import { ref } from 'vue';
  import TodoItem from './TodoItem.vue';
  import AddTodoButton from './AddTodoButton.vue';

  // Crée une variable réactive pour stocker la liste des tâches
  const todos = ref([]);

  // Fonction pour ajouter une tâche
  const addTodo = () => {
    // Crée une nouvelle tâche avec un ID unique et un texte par défaut
    const newTodo = {
      id: Date.now(), // Un identifiant unique
      text: "Nouvelle tâche",
      completed: false,
    };
    // Ajoute la nouvelle tâche à la fin de notre tableau
    todos.value.push(newTodo);
  };
</script>