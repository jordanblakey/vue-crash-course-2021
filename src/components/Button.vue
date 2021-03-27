<template>
  <button
    v-on:click="onClick()"
    @mouseover="onMouseOver()"
    :style="{ background: color }"
    class="btn"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: 'Header',
  props: {
    text: {
      type: String,
      default: 'Press Me'
    },
    color: {
      type: String,
      default: 'green'
    }
  },
  methods: {
    onClick() {
      // console.log('Click')
    },
    onMouseOver() {
      // console.log('MouseOver')
    }
  }
}
</script>
