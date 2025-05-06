<template>
  <div>
    <h1>Task Tracker</h1>
    <TaskForm @add-task="createTask" />
    <TaskList :tasks="tasks" @delete-task="deleteTask" @toggle-task="updateTask" />
  </div>
</template>

<script>
import TaskForm from '../components/TaskForm.vue';
import TaskList from '../components/TaskList.vue';
 import axios from 'axios';

export default {
  components: { TaskForm, TaskList },
  data() {
    return {
      tasks: []
    };
  },
  mounted() {
    this.fetchTasks();
  },
  methods: {
    fetchTasks() {
      axios.get('http://localhost:8080/api/tasks')
        .then(res => this.tasks = res.data);
    },
    createTask(task) {
      axios.post('http://localhost:8080/api/tasks', task)
        .then(res => this.tasks.push(res.data));
    },
    deleteTask(id) {
      axios.delete(`http://localhost:8080/api/tasks/${id}`)
        .then(() => this.tasks = this.tasks.filter(task => task.id !== id));
    },
    updateTask(task) {
      axios.put(`http://localhost:8080/api/tasks/${task.id}`, task);
    }
  }
};
</script>
