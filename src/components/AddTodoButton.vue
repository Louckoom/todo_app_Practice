<template>
  <v-container>
    <div class="d-flex justify-center my-4">
      <v-btn
        color="primary"
        size="large"
        prepend-icon="mdi-plus"
        @click="emit('add-todo')"
      >
        Ajouter une TO DO
      </v-btn>
    </div>
  </v-container>
</template>

<script setup>
  const emit = defineEmits(['add-todo']);
</script>