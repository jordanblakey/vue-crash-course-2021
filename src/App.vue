<template>
  <div class="container">
    <Header
      @toggle-add-task="toggleAddTask"
      :showAddTask="showAddTask"
      title="Task Tracker"
    />
    <div
      v-show="alertBox.active"
      :class="[{ active: alertBox.active }, 'alert-box']"
      :style="{ background: alertBox.color }"
    >
      {{ alertBox.message }}
    </div>
    <router-view
      :showAddTask="showAddTask"
      @toggle-add-task="toggleAddTask"
    ></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  data() {
    return {
      showAddTask: false,
      alertBox: {
        color: 'green',
        active: false,
        message: 'Task added.',
        fader: function() {
          this.active = true
          setTimeout(() => {
            this.active = false
          }, 2000)
        }
      }
    }
  },
  methods: {
    toggleAddTask(message) {
      if (typeof message !== 'undefined') {
        this.alertBox.fader()
      }

      this.showAddTask = !this.showAddTask
    }
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
  font-size: 16px;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid green;
  padding: 2rem;
}
.alert-box {
  color: white;
  font-weight: 700;
  padding: 1rem;
  margin: 5px 0 0;
}
.alert-box.active {
  opacity: 1;
  animation: fader 2s forwards;
}
@keyframes fader {
  0% {
    opacity: 1;
  }
  80% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:hover {
  opacity: 0.8;
}
.btn:active {
  opacity: 1;
}
.btn-block {
  display: block;
  width: 100%;
}
div,
input,
input:-webkit-autofill::first-line,
.btn {
  font-family: 'Poppins', sans-serif;
  font-size: 16px;
  border-radius: 5px;
}
input[type='text'] {
  border: 1px solid;
}
</style>
