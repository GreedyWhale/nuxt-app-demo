<template>
  <div class="container">
    <nav class="nav">
      <ul v-if="pageData.globalTags">
        <li
          v-for="(navItem, navIndex) in pageData.globalTags" :key="navItem.name"
          :class="{ active: navCurrentIndex === navIndex }"
          @click="toggleNav(navIndex)">
          {{ navItem.name }}
        </li>
      </ul>
    </nav>
    <main class="content">
      <div class="content-top">
        <p class="nav-desc">
          {{ pageData.globalTags[navCurrentIndex].summary }}
        </p>
        <ul class="top-three">
          <li
            v-for="num in 3"
            :key="pageData.rankingGlobals[num - 1].brandId"
            class="top-three-item"
            :style="{ width: pageData.rankingGlobals[num - 1].score + '%' }">
            <p>{{ `${num}.` }} {{ pageData.rankingGlobals[num - 1].brandName }}</p>
            <p>{{ pageData.rankingGlobals[num - 1].score }}</p>
          </li>
        </ul>
        <div class="open-app-tips">
          <img src="~/assets/icon/downArrow.png" alt="下箭头" class="down-arrow-icon">
          <p>打开App查看完整排行榜</p>
        </div>
      </div>
      <ul class="car-detail">
        <li
          v-for="carRank in 3" :key="pageData.rankingGlobals[carRank - 1].seq"
          class="car-detail-item">
          <div class="score-wrapper">
            <p class="score-title">分值</p>
            <p class="score">{{ pageData.rankingGlobals[carRank - 1].score }}</p>
            <img src="~/assets/img/rank-source.png" alt="排行来源" class="rank-source">
          </div>
          <div class="car-info">
            <p class="rank-num">
              {{ pageData.rankingGlobals[carRank - 1].seq.length > 1 ? pageData.rankingGlobals[carRank - 1].seq : `0${pageData.rankingGlobals[carRank - 1].seq}`}}
            </p>
            <p class="car-name">{{ pageData.rankingGlobals[carRank - 1].brandName }}</p>
            <p>/{{ pageData.rankingGlobals[carRank - 1].brand.country }}</p>
          </div>
          <article
            v-html="pageData.rankingGlobals[carRank - 1].comment" class="article"/>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pageData: {},
      navCurrentIndex: 0
    }
  },
  head() {
    return this.$seo(this.pageData.title, this.pageData.summary)
  },
  asyncData(context) {
    return context.$axios({
      method: 'post',
      url: '/guiderank-web/app/ranking/getRankingGlobalPage.do?ver=web_3.3.0',
      data: {
        categoryId: "",
        rankingId: "14827479311133655143"
      }
    })
    .then(res => {
      const synthesize = {
        name: '综合评分',
        summary: '综合评分指标说明：综合评分是根据驾驶、适用性、质量、安全、配置等各项影响20万+中型汽车品质的指标综合计算得出，综合评分越高表示该品牌综合品质越好。'
      }
      res.data.data.globalPage.globalTags.unshift(synthesize)
      return { pageData: res.data.data.globalPage }
    })
  },
  methods: {
    toggleNav(index) {
      this.navCurrentIndex = index
    }
  }
}
</script>

<style lang="scss">
  @import '~/assets/scss/var.scss';
  .container {
    .nav {
      background: #fff;
      > ul {
        display: flex;
        align-items: center;
        justify-content: space-around;
        border-bottom: 1px solid #ccc;
        > li {
          flex: none;
          text-align: center;
          color: #999;
          font-size: 0.16rem;
          cursor: pointer;
          padding: .2rem 0;
          position: relative;
          &.active {
            color: $lightblue;
            &::after {
              content: '';
              position: absolute;
              bottom: 0;
              left: 0;
              right: 0;
              height: .05rem;
              background: $lightblue;
            }
          }
        }
      }
    }
    .content {
      .content-top {
        padding: 0 .4rem;
        background: #fff;
        margin-bottom: .2rem;
        .nav-desc {
          font-size: .16rem;
          color: #999;
          padding-top: .2rem;
        }
        .top-three {
          margin-top: .4rem;
          &-item {
            font-size: .2rem;
            color: #fff;
            background: $lightblue;
            line-height: .5rem;
            padding: 0 .1rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            &:not(:last-child) {
              margin-bottom: .2rem;
            }
          }
        }
        .open-app-tips {
          .down-arrow-icon {
            display: block;
            margin: .4rem auto;
          }
          > p {
            font-size: .24rem;
            color: $lightblue;
            text-align: center;
            padding-bottom: .4rem;
          }
        }
      }
      .car-detail {
        .car-detail-item {
          padding: .2rem .4rem .4rem;
          background: #fff;
          &:not(:last-child) {
            margin-bottom: .2rem;
          }
          .score-wrapper {
            display: flex;
            align-items: center;
            color: $lightblue;
            margin-bottom: .3rem;
            .score-title {
              display: flex;
              align-items: center;
              justify-content: center;
              writing-mode: vertical-rl;
              font-size: .16rem;
              width: .32rem;
              height: .64rem;
              background: url('../assets/icon/score-bg.png') no-repeat center / cover;
            }
            .score {
              font-size: .64rem;
              margin: 0 .1rem;
            }
            .rank-source {
              height: .64rem; 
            }
          }
          .article {
            font-size: .3rem;
            color: #666;
            p {
              margin-bottom: .4rem;
            }
          }
          .car-info {
            display: flex;
            align-items: center;
            color: $lightblue;
            font-size: .24rem;
            margin-bottom: .2rem;
            .rank-num {
              flex: none;
              display: flex;
              align-items: center;
              justify-content: center;
              width: .32rem;
              height: .4rem;
              background: url('../assets/icon/score-bg.png') no-repeat center / 100% 100%;
            }
            .car-name {
              font-size: .35rem;
              margin: 0 .2rem;
            }
          }
        }
      }
    }
  }
</style>
