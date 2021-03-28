<template>
  <header>
    <router-link id="app-title" to="/">
      <h1>{{ title }}</h1>
    </router-link>
    <Button
      v-if="homePage"
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
  },
  computed: {
    homePage() {
      if (this.$route.path === '/') {
        return true
      }
    }
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

#app-title {
  text-decoration: none;
  color: black;
}
</style>
