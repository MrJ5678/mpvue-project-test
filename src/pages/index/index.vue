<template>
  <div>
    <div class="home" v-if="isAuth">
      <SearchBar
        :disabled="true"
        @onClick="onSearchBarClick"
        :hotSearch="hotSearch"
      >// 等价于直接写 disable
      </SearchBar>
      <HomeCard
        :data="homeCard"
        @onClick="onHomeBookClick"
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
          @onMoreClick="recommendChange('recommend')"
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
          @onMoreClick="recommendChange('freeRead')"
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
          @onMoreClick="recommendChange('hotBook')"
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
          @onMoreClick="onCategoryMoreClick"
          @onBookClick="onHomeBookClick"
        >
        </HomeBook>
      </div>
    </div>
    <Auth v-if=!isAuth @getUserInfo="init"></Auth>
  </div>
</template>

<script>
  import SearchBar from '../../components/home/SearchBar'
  import HomeCard from '../../components/home/HomeCard'
  import HomeBanner from '../../components/home/HomeBanner'
  import HomeBook from '../../components/home/HomeBook'
  import Auth from '../../components/base/Auth'
  import {getHomeData, recommend, freeRead, hotBook, register} from '../../api'
  import {getSetting, getUserInfo, setStorageSync, getStorageSync, getUserOpenId, showLoading, hideLoading} from '../../api/wechat'

  export default {
    components: {
      SearchBar,
      HomeCard,
      HomeBanner,
      HomeBook,
      Auth
    },
    data() {
      return {
        hotSearch: '',
        homeCard: {},
        banner: {},
        recommend: [],
        freeRead: [],
        hotBook: [],
        category: [],
        isAuth: true
      }
    },
    mounted() {
      // this.getHomeData()
      this.init()
    },
    methods: {
      recommendChange(key) {
        switch (key) {
          case 'recommend':
            recommend().then(response => {
              this.recommend = response.data.data
            })
            break
          case 'freeRead':
            freeRead().then(response => {
              this.freeRead = response.data.data
            })
            break
          case 'hotBook':
            hotBook().then(response => {
              this.hotBook = response.data.data
            })
            break
        }
      },
      onSearchBarClick() {
        this.$router.push({
          path: '/pages/search/main',
          query: {
            hotSearch: this.hotSearch
          }
        })
      },
      onBannerClick() {
        console.log('banner click...')
      },
      onCategoryMoreClick() {
        console.log('onMoreClick ...')
      },
      onHomeBookClick(book) {
        console.log(book)
        this.$router.push({
          path: '/pages/detail/main',
          query: {
            fileName: book.fileName
          }
        })
      },
      getSetting() {
        getSetting(
          'userInfo',
          () => {
            this.isAuth = true
            showLoading('正在加载')
            this.getUserInfo()
          },
          () => {
            this.isAuth = false
          }
        )
      },
      getHomeData(openId, userInfo) {
        getHomeData({openId}).then(response => {
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
            userInfo
          }
          hideLoading()
        }).catch(() => {
          hideLoading()
        })
      },
      getUserInfo() {
        const onOpenIdComplete = (openId, userInfo) => {
          this.getHomeData(openId, userInfo)
          register(openId, userInfo)
        }
        getUserInfo(
          (userInfo) => {
            console.log(userInfo)
            setStorageSync('userInfo', userInfo)
            const openId = getStorageSync('openId')
            if (!openId || openId.length === 0) {
              getUserOpenId(openId => onOpenIdComplete(openId, userInfo))
            } else {
              onOpenIdComplete(openId, userInfo)
            }
          },
          () => {
            console.log('failed...') // 获取用户信息，抛出异常
          }
        )
      },
      init() {
        this.getSetting()
      }
    }
  }
</script>

<style lang="scss" scoped>
</style>
