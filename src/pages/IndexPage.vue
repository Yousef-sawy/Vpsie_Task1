<template>
  <q-page class="flex flex-center">
    <q-card
      class="my-card text-white"
      style="background: radial-gradient(circle, #35a2ff 0%, #014a88 100%)"
    >
      <q-card-section>
        <div class="text-h4">To-do-list</div>
        <div class="text-subtitle2">by Yousef Ashraf</div>
      </q-card-section>

      <div class="row justify-center">
        <div class="col-8">
          <q-input
            v-model="newTask"
            placeholder="Add a new task"
            @keyup.enter="addTask"
            filled
            clearable
            class="q-mb-md input-white"
            :error="inputError"
            :error-message="'Task cannot be empty!'"
          />
        </div>
      </div>

      <q-separator dark inset />

      <q-card-section>
        <q-list bordered>
          <q-item v-for="(task, index) in tasks" :key="index" clickable v-ripple>
            <q-item-section>
              <q-input
                v-if="editIndex === index"
                v-model="editTask"
                @keyup.enter="finishEdit(index)"
                filled
                clearable
                class="input-white"
                :error="editError"
                :error-message="'Edited task cannot be empty!'"
              />
              <span v-else>{{ task }}</span>
            </q-item-section>
            <q-item-section side>
              <q-btn dense flat round icon="edit" @click="startEdit(index)" class="text-white" />
              <q-btn dense flat round icon="delete" @click="removeTask(index)" class="text-white" />
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';

const newTask = ref('');
const tasks = ref([]);
const editTask = ref('');
const editIndex = ref(null);
const inputError = ref(false);
const editError = ref(false);

onMounted(() => {
  const storedTasks = JSON.parse(localStorage.getItem('tasks'));
  if (storedTasks) {
    tasks.value = storedTasks;
  }
});

watch(tasks, (newTasks) => {
  localStorage.setItem('tasks', JSON.stringify(newTasks));
}, { deep: true });

function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push(newTask.value.trim());
    newTask.value = '';
    inputError.value = false;
  } else {
    inputError.value = true;
  }
}

function removeTask(index) {
  tasks.value.splice(index, 1);
}

function startEdit(index) {
  editIndex.value = index;
  editTask.value = tasks.value[index];
  editError.value = false;
}

function finishEdit(index) {
  if (editTask.value.trim()) {
    tasks.value[index] = editTask.value.trim();
    editIndex.value = null;
    editTask.value = '';
    editError.value = false;
  } else {
    editError.value = true;
  }
}
</script>

<style scoped>
.my-card {
  max-width: 500px;
  width: 100%;
}

.text-white {
  color: white !important;
}

.input-white {
  color: white !important;
}

.input-white .q-field__native {
  color: white !important;
}

.input-white ::placeholder {
  color: white !important; 
  opacity: 1;
}
</style>
