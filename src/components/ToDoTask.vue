<template>
    <tr class="display">
      <td class="task-container">
        <input type="checkbox" v-model="task.fait" class="task-checkbox">
        <span :class="{ 'completed-task': task.fait }">{{ task.nom }}</span>
        <button @click="$emit('delete', task.id)" class="delete-button">Supprimer</button>
      </td>
    </tr>
  </template>
  
  <style scoped>
  .task-container {
    display: flex; 
    align-items: center;
    justify-content: space-between;
    width: 100%;
  }
  
  .task-checkbox {
    margin-right: 10px;
  }
  
  .completed-task {
    text-decoration: line-through;
  }
  
  .delete-button {
    margin-left: auto; 
    padding: 5px 10px;
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .delete-button:hover {
    background-color: #d32f2f;
  }

  .display {
    display: contents;
  }

  </style>
  
  
  
  <script>
  export default {
    name: 'ToDoTask',
    props: {
      task: Object
    }
  }
  </script>
  