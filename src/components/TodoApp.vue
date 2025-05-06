<script setup>
import { ref, computed } from 'vue';

const activities = ref([]);
const newActivity = ref("");
const showOnlyIncomplete = ref(false);

// Fungsi menambahkan kegiatan baru
const addActivity = () => {
  if (newActivity.value.trim()) {
    activities.value.push({ text: newActivity.value, completed: false });
    newActivity.value = "";
  }
};
</script>

<template>
 <div class="todo-app">
  <div class="todo-input">
      <input
        v-model="newActivity"
        type="text"
        placeholder="Add New Activities" />
      <button @click="addActivity">Add</button>
    </div>

 </div>

</template>