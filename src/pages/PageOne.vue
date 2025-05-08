<template>
  <q-page class="flex flex-center">
    <q-card dark bordered class="bg-grey-9 my-card">
      <q-card-section>
        <div class="text-h4">Inspirational Quotes</div>
        <!-- <div class="text-subtitle2">by Yousef Ashraf</div> -->
      </q-card-section>

      <q-separator dark inset />

      <q-card-section>
        <div v-if="loading" class="loading">
          Loading...
        </div>
        <div v-else class="quote-display q-my-md">
          "{{ currentQuote.content }}" – {{ currentQuote.author }}
        </div>
        <q-btn label="Show Another Quote" @click="fetchQuote" color="primary" />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { api } from 'src/boot/axios';

const currentQuote = ref({});
const loading = ref(false);

// Function to fetch a quote from the API
async function fetchQuote() {
  loading.value = true;
  try {
    const response = await api.get('/random');
    currentQuote.value = response.data;
  } catch (error) {
    console.error('Error fetching quote:', error);
    currentQuote.value = {
      content: 'Failed to fetch quote. Please try again.',
      author: '',
    };
  } finally {
    loading.value = false;
  }
}

onMounted(fetchQuote);
</script>

<style scoped>
.my-card {
  max-width: 600px;
  width: 100%;
  text-align: center;
}

.quote-display {
  font-style: italic;
  margin-bottom: 20px;
}

.loading {
  margin-bottom: 20px;
}
</style>
