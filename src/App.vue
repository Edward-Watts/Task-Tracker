<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :alterAddTask="showAddTask" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder"
        @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',

  components: {
    Header,
    Tasks,
    AddTask,
  },

  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    addTask(task) {
      this.tasks= [...this.tasks, task]
    },

    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },

    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks= this.tasks.filter((task) => task.id !== id)
      }
    },

    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id ===id 
        ? {...task, reminder: !task.reminder} : task)
    }
  },

  created() {
    this.tasks = [
      {
      id: 1,
      text: 'Doctors Appointment',
      day: 'December 1 at 01:00pm',
      reminder: true
    },
    {
      id: 2,
      text: 'Visit Site',
      day: 'December 3 at 09:30am',
      reminder: true
    },
    {
      id: 3,
      text: 'Study Vue.js',
      day: 'December 3 at 04:00pm',
      reminder: false
    }
    ]
  }
}
</script>



<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  text-align: inherit;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}
</style>
