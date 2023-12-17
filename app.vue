<template>
  <div>
    <h1>Vue 3 + Nuxt.js To-Do List</h1>
    <div>
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task">
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <span :class="{ 'completed': task.completed }">{{ task.title }}</span>
          <button v-if="task.completed" @click="toggleTask(index)">Mark as undone</button>
          <button v-else @click="toggleTask(index)">Mark as done</button>
          <button @click="removeTask(index)">Remove</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTask = ref('');
    const tasks = ref([]);
    

    const addTask = () => {
      if (newTask.value.trim() !== '') {
        tasks.value.push({ title: newTask.value, completed: false });
        newTask.value = '';
      }
    };

    const toggleTask = (index) => {
      tasks.value[index].completed = !tasks.value[index].completed;
    };

    const removeTask = (index) => {
      tasks.value.splice(index, 1);
    };

    return {
      newTask,
      tasks,
      addTask,
      toggleTask,
      removeTask,
    };
  },
};
</script>

<style>
#app {
  font-family: 'Arial', sans-serif;
  text-align: center;
  margin-top: 50px;
}

h1 {
  color: #333;
}

div {
  max-width: 400px;
  margin: 0 auto;
}

input {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  margin-bottom: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  margin-bottom: 5px;
  padding: 10px;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

button {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 8px 12px;
  cursor: pointer;
}

button:hover {
  background-color: #c82333;
}
</style>
