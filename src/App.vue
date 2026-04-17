<script setup>
  import {ref} from 'vue';

  const newTask = ref('');
  const tasks = ref([]);

  function addTask(){
    if(newTask.value.trim() === '') return;
    tasks.value.push({
      id: Date.now(),
      text: newTask.value,
      done: false
    });
    newTask.value = '';
  }

  function toggleTask(task){
    task.done = !task.done;
  }

  function deleteTask(id){
    tasks.value = tasks.value.filter(task => task.id !== id)
  }

</script>

<template>
  <h1>To-Do List Practice</h1>
  <input 
    v-model="newTask"
    @keyup.enter="addTask"
    placeholder="What needs doing?" 
  />
  <button @click="addTask">Add</button>

  <ul>
    <li 
      v-for="task in tasks" 
      :key="task.id">
        <span
          @click="toggleTask(task)"
          :class="{done: task.done}"
          >
            {{task.text}}
        </span>
        <button @click="deleteTask(task.id)">✕</button>
    </li>
  </ul>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
    color: gray;
  }
</style>