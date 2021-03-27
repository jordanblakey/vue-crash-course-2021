<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      @click="$emit('toggle-add-task')"
      :text="showAddTask ? 'Cancel' : 'Add Task'"
      :color="showAddTask ? 'grey' : 'green'"
    />
  </header>
</template>

<script>
import Button from './Button'

export default {
  name: 'Header',
  props: {
    title: {
      type: String,
      default: 'Hello World'
    },
    showAddTask: {
      type: Boolean,
      default: false
    }
  },
  components: {
    Button
  }
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
