<template>
  <div>
    <h2>Add Task</h2>
    <form @submit.prevent="addTask">
      <input v-model="title" placeholder="Title" required />
      <input v-model="description" placeholder="Description" required />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      description: ''
    };
  },
  methods: {
    addTask() {
      const task = {
        title: this.title,
        description: this.description,
        completed: false
      };
      this.$emit('add-task', task);
      this.title = '';
      this.description = '';
    }
  }
};
</script>
