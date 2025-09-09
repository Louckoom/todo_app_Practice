<template>
  <v-app>
    <Header />
    <v-main>
      <v-container>
        <AddTodoButton @add-todo="addTodo" />
        <TodoList 
          :todos="mainTodos"
          @check-todo="checkTodo"
          @delete-todo="deleteTodo"
          @add-sub-todo="addSubTodo"
        />
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
  import { ref, watch, onMounted } from 'vue';
  import Header from './components/Header.vue';
  import TodoList from './components/TodoList.vue';
  import AddTodoButton from './components/AddTodoButton.vue';

  const mainTodos = ref([]);

  // FONCTIONS UTILITAIRES POUR PARCOURIR L'ARBRE DE TÂCHES
  // Ces fonctions sont réutilisables et gèrent la logique récursive
  function findTodoInTree(list, id) {
    for (const item of list) {
      if (item.id === id) {
        return item;
      }
      if (item.subTodos && item.subTodos.length > 0) {
        const found = findTodoInTree(item.subTodos, id);
        if (found) {
          return found;
        }
      }
    }
    return null;
  }

  function deleteTodoInTree(list, id) {
    return list.filter(t => {
      if (t.id === id) {
        return false;
      }
      if (t.subTodos && t.subTodos.length > 0) {
        t.subTodos = deleteTodoInTree(t.subTodos, id);
      }
      return true;
    });
  }

  // GESTION D'ÉTAT PRINCIPALE
  // Gère la persistance des données dans le localStorage
  onMounted(() => {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      mainTodos.value = JSON.parse(savedTodos);
    }
  });

  watch(
    mainTodos,
    (newTodos) => {
      localStorage.setItem('todos', JSON.stringify(newTodos));
    },
    { deep: true }
  );

  // FONCTIONS DE L'APPLICATION
  // Gèrent les événements émis par les composants enfants
  const addTodo = () => {
  const newTodo = {
    id: Date.now(),
    text: 'Nouvelle tâche',
    completed: false,
    subTodos: []
  };
  mainTodos.value.unshift(newTodo);
};

  const checkTodo = (id) => {
    const todo = findTodoInTree(mainTodos.value, id);
    if (todo) {
      todo.completed = !todo.completed;
      // Met à jour les sous-tâches si la tâche parente est cochée ou décochée
      if (todo.completed) {
          checkAllSubTodos(todo.subTodos, true);
      } else {
          checkAllSubTodos(todo.subTodos, false);
      }
    }
  };

  const deleteTodo = (id) => {
    mainTodos.value = deleteTodoInTree(mainTodos.value, id);
  };

  const addSubTodo = (parentId) => {
  const parentTodo = findTodoInTree(mainTodos.value, parentId);
  if (parentTodo) {
    const newSubTodo = {
      id: Date.now(),
      text: 'Nouvelle sous-tâche',
      completed: false,
      subTodos: []
    };
    parentTodo.subTodos.push(newSubTodo);
  }
};

  const checkAllSubTodos = (subTodos, status) => {
    for (const subTodo of subTodos) {
      subTodo.completed = status;
      if (subTodo.subTodos.length > 0) {
        checkAllSubTodos(subTodo.subTodos, status);
      }
    }
  };
</script>