<template>
  <div class='container'>
    <Header @toggle-add="toggleAdd" title='Task Tracker' :showAddTask='this.showAddTask' />

    <div v-show='showAddTask'>
      <AddTask @add-task="addTask" />
    </div>

    <Tasks @delete-task="deleteTask" @toggle-reminder='toggleReminder' :tasks="tasks" />
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    toggleAdd() {
      this.showAddTask = !this.showAddTask
    },
    deleteTask(taskId) {
      console.log('task', taskId)
      if(confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(task => {
          return task.id != taskId
        })
      }
    },
    toggleReminder(taskId) {
      console.log('Toggling reminder', taskId)

      this.tasks = this.tasks.map(task => {
        if (task.id === taskId) {
          task.reminder = !task.reminder
        }

        return task
      })
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctor',
        day: 'March 1st at 2:30pm',
        reminder: true
      }, {
        id: 2,
        text: 'School',
        day: 'March 1st at 4:30pm',
        reminder: false
      }, {
        id: 3,
        text: 'Food',
        day: 'March 1st at 6:30pm',
        reminder: false
      }
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
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

.btn-block {
  display: block;
  width: 100%;
}
</style>