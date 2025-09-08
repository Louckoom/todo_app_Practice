<template>
  <v-app-bar app color="primary" dark>
    <v-toolbar-title>TO DO APP</v-toolbar-title>

    <v-spacer></v-spacer>

    <v-text-field
      density="compact"
      variant="solo"
      label="Search..."
      prepend-inner-icon="mdi-magnify"
      single-line
      hide-details
    ></v-text-field>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn icon v-bind="props">
          <v-icon>mdi-sort</v-icon>
        </v-btn>
      </template>
      <v-list>
        <v-list-item>
          <v-list-item-title>Alphabetical</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-title>By date</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>

    <v-menu>
      <template v-slot:activator="{ props }">
        <v-btn icon v-bind="props">
          <v-icon>mdi-group</v-icon>
        </v-btn>
      </template>
      <v-list>
        <v-list-item>
          <v-list-item-title>Completed</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-title>In progress</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </v-app-bar>
</template>

<script setup>
// Pour l'instant on laisse vide
</script>