<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input v-model="text" type="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        v-model="day"
        type="text"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input v-model="reminder" type="checkbox" name="reminder" />
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>
<script>
export default {
  name: 'AddTask',
  data() {
    return {
      text: '',
      day: '',
      reminder: false
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()
      if (!this.text) {
        alert('Please add a task')
        return
      }

      let validDate = new Date(this.day)
      if (validDate.toString() === 'Invalid Date') {
        alert('Enter a numeric date and time (e.g. 2021-03-25 12:00).')
        return
      }
      validDate = validDate.toISOString()

      const newTask = {
        id: Math.floor(Math.random() * 100000),
        text: this.text,
        day: validDate,
        reminder: this.reminder
      }

      this.$emit('add-task', newTask)

      this.text = ''
      this.day = ''
      this.reminder = false
    }
  }
}
</script>
<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px 0;
  padding: 3px 7px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.form-control-check label {
  margin-right: 10px;
}
.form-control-check input {
  height: 20px;
  width: 20px;
}
</style>
