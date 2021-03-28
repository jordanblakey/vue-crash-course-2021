<template>
  <div v-show="showAddTask">
    <AddTask @add-task="addTask" />
  </div>
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
  <p
    v-if="tipOfTheDay"
    class="tip"
    title="Dismiss tip of the day"
    @click="tipOfTheDay = undefined"
  >
    {{ tipOfTheDay }}
  </p>
</template>
<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'

export default {
  name: 'Home',
  components: {
    Tasks,
    AddTask
  },
  props: {
    showAddTask: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      tasks: [],
      tipOfTheDay: undefined,
      showTip: true
    }
  },
  methods: {
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(task)
      })
      const data = await res.json()

      console.info('Added task:', data)

      this.tasks = [...this.tasks, data]
      // this.alertBox.fader()
      this.$emit('toggle-add-task', { message: 'Task added.', color: 'green' })
    },
    async deleteTask(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        })
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id != id))
          : alert('Error deleting task!')
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder }
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(updateTask)
      })
      const data = await res.json()

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      )
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')
      const data = res.json()
      return data
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)
      const data = res.json()
      return data
    },
    async fetchTips() {
      const res = await fetch('api/tips')
      const data = res.json()
      return data
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
    let tips = await this.fetchTips()
    this.tipOfTheDay = tips[Math.floor(Math.random() * tips.length)].text
  },
  emits: ['toggle-add-task']
}
</script>
<style scoped>
.tip {
  text-align: center;
  margin-top: 1rem;
  cursor: help;
}
::selection {
  background: hotpink;
}
</style>
