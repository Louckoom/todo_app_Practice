<template>
  <v-card
    class="mx-auto bordered mb-4"
    max-width="800"
    variant="flat"
    :class="{ 'completed-card': todo.completed }"
  >
    <v-card-text class="d-flex align-center">
      <span
        v-if="!isEditing"
        class="text-h6 editable-text"
        @click="isEditing = true"
        :class="{ 'completed-text': todo.completed }"
      >
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

      <v-btn
        v-if="!isEditing"
        icon
        color="green"
        class="mx-1"
        @click="emit('check-todo', todo.id)"
      >
        <v-icon>mdi-check-circle-outline</v-icon>
      </v-btn>

      <v-btn
        v-if="!isEditing"
        icon
        color="red"
        class="mx-1"
        @click="emit('delete-todo', todo.id)"
      >
        <v-icon>mdi-close-circle-outline</v-icon>
      </v-btn>

      <v-btn v-if="!isEditing" icon color="blue" class="mx-1" @click="emit('add-sub-todo', todo.id)">
        <v-icon>mdi-plus-circle-outline</v-icon>
      </v-btn>
    </v-card-text>
    
    <v-card-text v-if="todo.subTodos && todo.subTodos.length > 0" class="pl-12">
        <TodoItem
          v-for="subTodo in todo.subTodos"
          :key="subTodo.id"
          :todo="subTodo"
          @check-todo="emit('check-todo', $event)"
          @delete-todo="emit('delete-todo', $event)"
          @add-sub-todo="emit('add-sub-todo', $event)"
        />
    </v-card-text>
  </v-card>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  todo: Object,
});

const emit = defineEmits(['check-todo', 'delete-todo', 'add-sub-todo']);

const isEditing = ref(false);

const saveEdit = () => {
  isEditing.value = false;
};
</script>

<style scoped>
/* styles... */
</style>