<template>
  <v-app>
    <v-main>
      <Header />
      <TodoList />
    </v-main>
  </v-app>
</template>

<script setup>
import Header from './components/Header.vue';
import TodoList from './components/TodoList.vue';
</script>

<style scoped>
/* On peut laisser vide aussi */
</style>