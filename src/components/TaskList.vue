<template>
  <div>
    <h2>Tasks</h2>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input type="checkbox" v-model="task.completed" @change="toggleTask(task)" />
        {{ task.title }} - {{ task.description }}
        <button @click="deleteTask(task.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: ['tasks'],
  emits: ['delete-task', 'toggle-task'],
  methods: {
    deleteTask(id) {
      this.$emit('delete-task', id);
    },
    toggleTask(task) {
      this.$emit('toggle-task', task);
    }
  }
};
</script>
