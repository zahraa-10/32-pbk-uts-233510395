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

// Fungsi untuk membatalkan (menghapus) kegiatan
const cancelActivity = (index) => {
  activities.value.splice(index, 1);
};

// Fungsi untuk toggle (menceklist) kegiatan selesai
const toggleComplete = (index) => {
  activities.value[index].completed = !activities.value[index].completed;
};

// Computed property untuk memfilter kegiatan
const filteredActivities = computed(() => {
  return showOnlyIncomplete.value
    ? activities.value.filter(activity => !activity.completed)
    : activities.value;
});
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

    <div class="todo-filter">
      <label>
        <input type="checkbox" v-model="showOnlyIncomplete" />
        Show only unfinished activities
      </label>
    </div>
    <ul class="todo-list">
      <li v-for="(activity, index) in filteredActivities" :key="index" class="activity-item">
        <input 
          type="checkbox" 
          :checked="activity.completed"
          @change="toggleComplete(index)" />
        <span :class="{ completed: activity.completed }">
          {{ activity.text }}
        </span>
        <button class="delete-btn" @click="cancelActivity(index)">Delete</button>
      </li>
    </ul>
  </div>

</template>