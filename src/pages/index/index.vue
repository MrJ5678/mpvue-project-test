<template>
  <div class="home">
    <SearchBar
      :disabled="true"
      @onClick="onSearchaBarClick"
      :hotSearch="hotSearch"
    >// 等价于直接写 disable
    </SearchBar>
    <HomeCard
      :data="homeCard"
    >
    </HomeCard>
    <HomeBanner
      img="http://www.youbaobao.xyz/book/res/bg.jpg"
      title="mpvue 2.0项目开发测试"
      subTitle="开始测试"
      @onClick="onBannerClick"
    >
    </HomeBanner>
    <div :style="{marginTop: '23px'}">
      <HomeBook
        :row="1"
        :col="3"
        title="为你推荐"
        :data="recommend"
        mode="col"
        btn-text="换一批"
        @onMoreClick="onBookMoreClick"
        @onBookClick="onHomeBookClick"
      >
      </HomeBook>
    </div>
    <div :style="{marginTop: '23px'}">
      <HomeBook
        :row="2"
        :col="2"
        title="免费阅读"
        :data="freeRead"
        mode="row"
        btn-text="换一批"
        @onMoreClick="onBookMoreClick"
        @onBookClick="onHomeBookClick"
      >
      </HomeBook>
    </div>
    <div :style="{marginTop: '23px'}">
      <HomeBook
        :row="1"
        :col="4"
        title="当前最热"
        :data="hotBook"
        mode="col"
        btn-text="换一批"
        @onMoreClick="onBookMoreClick"
        @onBookClick="onHomeBookClick"
      >
      </HomeBook>
    </div>
    <div :style="{marginTop: '23px'}">
      <HomeBook
        :row="3"
        :col="2"
        title="分类"
        :data="category"
        mode="category"
        btn-text="查看全部"
        @onMoreClick="onBookMoreClick"
        @onBookClick="onHomeBookClick"
      >
      </HomeBook>
    </div>
  </div>
</template>

<script>
  import SearchBar from '../../components/home/SearchBar'
  import HomeCard from '../../components/home/HomeCard'
  import HomeBanner from '../../components/home/HomeBanner'
  import HomeBook from '../../components/home/HomeBook'
  import { getHomeData } from '../../api'

  export default {
    components: {
      SearchBar,
      HomeCard,
      HomeBanner,
      HomeBook
    },
    data() {
      return {
        hotSearch: '',
        homeCard: {},
        banner: {},
        recommend: [],
        freeRead: [],
        hotBook: [],
        category: []
      }
    },
    mounted() {
      console.log(this.getHomeData())
    },
    methods: {
      getHomeData() {
        getHomeData({openId: 1234}).then(response => {
          const {
            data: {
              hotSearch: {
                keyword
              },
              shelf,
              banner,
              recommend,
              freeRead,
              hotBook,
              category,
              shelfCount
            }
          } = response.data
          console.log(keyword, shelf, banner, recommend, freeRead, hotBook, category, shelfCount)
          this.hotSearch = keyword
          this.shelf = shelf
          this.banner = banner
          this.recommend = recommend
          this.freeRead = freeRead
          this.hotBook = hotBook
          this.category = category
          this.homeCard = {
            bookList: shelf,
            num: shelfCount,
            userInfo: {
              avatar: 'https://www.youbaobao.xyz/mpvue-res/logo.jpg',
              nickname: '米老鼠'
            }
          }
        })
      },
      onSearchaBarClick() {
        //  跳转到搜索页面

      },
      onBannerClick() {
        console.log('banner click...')
      },
      onBookMoreClick() {
        console.log('onMoreClick ...')
      },
      onHomeBookClick() {
        console.log('onBookClick ...')
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>
