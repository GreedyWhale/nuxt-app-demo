<template>
  <section class="container">
    <div>
      <logo/>
      <h1 class="title">
        nuxt-app
      </h1>
      <h2 class="subtitle">
        My ultimate Nuxt.js project
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green">Documentation</a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey">GitHub</a>
      </div>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  data() {
    pageData: {}
  },
  components: {
    Logo
  },
  asyncData(context) {
    return context.$axios({
      method: 'post',
      url: '/guiderank-web/app/ranking/getRankingGlobalPage.do?ver=web_3.3.0',
      data: JSON.stringify({
        categoryId: "",
        rankingId: "14827479311133655143"
      })
    })
    .then(res => {
      console.log(res)
    })
  },
  created() {
    this.$axios({
      method: 'post',
      url: '/guiderank-web/app/ranking/getRankingGlobalPage.do?ver=web_3.3.0',
      data: {
        categoryId: "",
        rankingId: "14827479311133655143"
      }
    })
    .then(res => {
      console.log(res)
    })
  },
}
</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
