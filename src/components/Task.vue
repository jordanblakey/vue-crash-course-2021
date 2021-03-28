<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <div>
      <h3>
        {{ task.text }}
      </h3>
      <p>{{ displayDate }}</p>
    </div>
    <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object
  },
  computed: {
    displayDate: function() {
      let d = new Date(this.$props.task.day)
      if (d.toString() !== 'Invalid Date') {
        return d.toLocaleDateString() + ' at ' + d.toLocaleTimeString()
      } else return this.$props.task.day
    }
  }
}
</script>

<style scoped>
.fas {
  color: red;
  font-size: 20px;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.task {
  background: #f4f4f4;
  margin: 5px 0;
  padding: 10px 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task.reminder {
  border-left: 5px solid green;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
