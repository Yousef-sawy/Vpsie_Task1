<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          {{ headerTitle }}
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs align="left">
        <q-route-tab to="/" label="ToDoList" />
        <q-route-tab to="/page1" label="Inspirational Quotes" />
        <q-route-tab to="/page2" label="Calendar" />
        <q-route-tab to="/page3" label="Page Three(not working)" />
      </q-tabs>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref, watch } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const headerTitle = ref('Task 1 (ToDoList)'); // Default title

watch(route, () => {
  switch (route.path) {
    case '/':
      headerTitle.value = 'Task 1 (ToDoList)';
      break;
    case '/page1':
      headerTitle.value = 'Inspirational Quotes';
      break;
    case '/page2':
      headerTitle.value = 'Calendar';
      break;
    case '/page3':
      headerTitle.value = 'Page Three Title';
      break;
    default:
      headerTitle.value = 'Task 1 (ToDoList)';
  }
});
</script>
