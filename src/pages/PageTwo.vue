<template>
  <q-page class="flex flex-center">
    <q-card dark bordered class="bg-grey-9 my-card">
      <q-card-section>
        <div class="text-h4">Calendar</div>
        <div class="text-subtitle2">by Yousef Ashraf</div>
      </q-card-section>

      <q-separator dark inset />

      <q-card-section>
        <vue-cal
          class="vuecal--no-border"
          :events="events"
          style="height: 600px"
        />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import VueCal from 'vue-cal';
import 'vue-cal/dist/vuecal.css';

</script>

<style scoped>
.my-card {
  max-width: 800px;
  width: 100%;
}
</style>
