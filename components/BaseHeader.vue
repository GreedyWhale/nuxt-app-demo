<template>
  <header class="base-header">
     <nav class="nav">
      <ul>
        <li
          v-for="(item, index) in navList" :key="item.name"
          :class="{ active: navCurrentIndex === index }"
          @click="toggleNav(index)">
           <nuxt-link :to="item.path">{{ item.name }}</nuxt-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'BaseHeader',
  data() {
    return {
      navList: [
        { name: '综合榜', path: '/' },
        { name: '特色榜', path: '/featuresList' },
        { name: '人气榜', path: '/sentimentList' },
        { name: '知识百科', path: '/wikipedia' },
      ],
       navCurrentIndex: 0
    }
  },
  methods: {
    toggleNav(index) {
      this.navCurrentIndex = index
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~/assets/scss/var.scss';

.base-header {
  .nav {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    background: #f5f5f5;
    padding: 0 .2rem;
    z-index: 1;
    > ul {
      display: flex;
      align-items: center;
      height: 1.5rem;
      box-sizing: border-box;
      > li {
        flex: 1;
        text-align: center;
        line-height: .6rem;
        color: #333;
        font-size: .16rem;
        border-top: 1px solid #ccc;
        border-bottom: 1px solid #ccc;
        border-right: 1px solid #ccc;
        &:first-child {
          border-left: 1px solid #ccc;
        }
        &.active {
          background: $lightblue;
          border-color: $lightblue;
          color: #fff;
        }
      }
    }
  }
}
</style>
