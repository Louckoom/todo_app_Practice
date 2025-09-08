<template>
  <v-card class="mx-auto bordered mb-4" max-width="800" variant="flat">
    <v-card-text class="d-flex align-center">
      <span v-if="!isEditing" class="text-h6 editable-text" @click="isEditing = true">
        {{ todo.text }}
      </span>

      <v-form v-if="isEditing" class="d-flex align-center flex-grow-1">
        <v-text-field
          v-model="todo.text"
          variant="solo"
          autofocus
          hide-details
          class="flex-grow-1"
        ></v-text-field>

        <v-btn icon size="small" color="primary" @click="saveEdit" class="ml-2">
          <v-icon>mdi-check</v-icon>
        </v-btn>
      </v-form>

      <v-spacer></v-spacer>

      <v-btn icon color="green" class="mx-1">
        <v-icon>mdi-check-circle-outline</v-icon>
      </v-btn>

      <v-btn icon color="red" class="mx-1">
        <v-icon>mdi-close-circle-outline</v-icon>
      </v-btn>

      <v-btn icon color="blue" class="mx-1">
        <v-icon>mdi-plus-circle-outline</v-icon>
      </v-btn>
    </v-card-text>
  </v-card>
</template>

<script setup>
  import { ref } from 'vue';

  const props = defineProps({
    todo: Object,
  });

  const isEditing = ref(false);

  const saveEdit = () => {
    isEditing.value = false;
  };
</script>

<style scoped>
  .bordered {
    border-bottom: 1px solid rgba(0, 0, 0, 0.12);
  }

  .editable-text {
    cursor: pointer;
    padding: 10px; /* Ajout d'un padding pour un meilleur effet visuel */
    transition: background-color 0.3s ease;
    border-radius: 4px;
  }
  .editable-text:hover {
    background-color: #f5f5f5; /* Un gris très clair */
  }
</style>