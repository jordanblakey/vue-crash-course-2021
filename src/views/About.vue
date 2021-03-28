<template>
  <div class="about">
    <h3>
      {{ aboutInfo.appName }}
      <small>Version {{ aboutInfo.version }} ({{ aboutInfo.release }})</small>
    </h3>
    <router-link to="/">Got it!</router-link>
  </div>
</template>
<script>
export default {
  name: 'About',
  data() {
    return {
      aboutInfo: {
        version: undefined
      }
    }
  },
  methods: {
    async getAboutInfo() {
      const res = await fetch('api/about')
      const data = res.json()
      return data
    }
  },
  async created() {
    this.aboutInfo = await this.getAboutInfo()
  }
}
</script>
<style scoped>
.about {
  padding: 1rem 0;
  margin-top: 1rem;
  border: 1px dotted green;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
