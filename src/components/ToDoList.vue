<template>
    <div class="container">
        <p>Tâches réalisées : <span class="completed-task">{{ completedCount }}</span> sur {{ tasks.length }}</p>
      <form class="form-container" @submit.prevent="ajouter">
        <input type="text" v-model="nouvelleTache" placeholder="Ajoutez une nouvelle tâche" class="input-new-task">
        <button type="submit" class="add-button">Ajouter</button>
      </form>
      <div class="progress-bar">
        <progress :value="completedPercentage" max="100"></progress>
        <span class="completed-task">{{ completedPercentage }}%</span>
      </div>
      <table class="tasks-table">
        <tr v-for="(task, index) in tasks" :key="task.id">
          <ToDoTask :task="task" @delete="supprimer(index)"/>
        </tr>
      </table>
    </div>
  </template>
  
  <style scoped>
  .container {
    width: 80%;
    max-width: 80%;
    margin: 50px auto;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    text-align: center;
  }

  .completed-task {
    color: #0075FF;
    font-weight: bold;
  }

  .form-container {
    display: flex;
    justify-content: center;
    gap: 12px;
  }
  
  .input-new-task, .add-button {
    padding: 10px;
    margin: 10px 0;
    border-radius: 5px;
    border: solid rgba(128, 128, 128, 0.39) 1px;
  }

  .add-button {
    background-color: #0075FF;
  }
  .add-button:hover {
    background-color: #0765d0;
  }
  
  .progress-bar {
    width: 100%;
    padding: 10px 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  progress {
    width: 100%;
    height: 40px;
    margin-right: 10px;
  }
  
  .tasks-table {
    width: 100%;
    margin-top: 20px;
    border-collapse: collapse;
  }
  
  .tasks-table td, .tasks-table th {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  
  .tasks-table tr:nth-child(even){background-color: #f2f2f2;}
  
  .tasks-table tr:hover {background-color: #ddd;}
  
  .tasks-table th {
    padding-top: 12px;
    padding-bottom: 12px;
    background-color: #4CAF50;
    color: white;
  }
  </style>
  
  
  <script>
  import axios from 'axios';
  import ToDoTask from './ToDoTask.vue';
  
  export default {
    name: 'ToDoList',
    components: {
      ToDoTask
    },
    data() {
      return {
        tasks: [],
        nouvelleTache: ''
      };
    },
    computed: {
      completedCount() {
        return this.tasks.filter(task => task.fait).length;
      }
    },
    methods: {
      loadTasks() {
        axios.get('https://jsonplaceholder.typicode.com/todos')
          .then(response => {
            this.tasks = response.data.map(item => ({
              id: item.id,
              nom: item.title,
              fait: item.completed
            }));
          })
          .catch(error => console.error('Erreur de chargement des tâches:', error));
      },
      ajouter() {
        if (this.nouvelleTache !== '') {
          this.tasks.push({
            id: this.tasks.length + 1,
            nom: this.nouvelleTache,
            fait: false
          });
          this.nouvelleTache = '';
        }
      },
      supprimer(index) {
        this.tasks.splice(index, 1);
      }
    },
    computed: {
        completedCount() {
            return this.tasks.filter(task => task.fait).length;
        },
        completedPercentage() {
            if (this.tasks.length === 0) return 0;
            return Math.round((this.completedCount / this.tasks.length) * 100);
        }
    },
    mounted() {
      this.loadTasks();
    }
  }
  </script>
  