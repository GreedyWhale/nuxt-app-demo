<template>
  <div>
    <base-header />
    <nuxt/>
  </div>
</template>

<script>
import BaseHeader from '~/components/BaseHeader.vue'

export default {
  components: {
    BaseHeader
  },
  mounted() {
  
  },
}
</script>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

body {
  padding-top: 1.5rem;
}
</style>
