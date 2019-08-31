<template>
  <div>
    <SearchBar
      :focus="searchFocus"
      :hotSearch="hotSearchKeyWord"
      @onChange="onChange"
      @onClear="onClear"
      @onConfirm="onConfirm"
      ref="searchBar"
    >
    </SearchBar>
    <TagGroup
      header-text="热门搜索"
      btn-text="换一批"
      :value="hotSearchArray"
      @onBtnClick="changeHotSearch"
      @onTagClick="showBookDetail"
      v-if="hotSearchArray.length > 0 && !showList"
    >
    </TagGroup>
    <TagGroup
      header-text="历史搜索"
      btn-text="清空"
      :value="historySearch"
      @onBtnClick="clearHistorySearch"
      @onTagClick="searchKeyWord"
      v-if="historySearch.length > 0 && !showList"
    >
    </TagGroup>
    <SearchList
      :data="searchList"
      v-if="showList"
    >
    </SearchList>
  </div>
</template>

<script>
  import SearchBar from '../../components/home/SearchBar'
  import TagGroup from '../../components/base/TagGroup'
  import SearchList from '../../components/search/SearchList'
  import {getStorageSync, setStorageSync, showToast} from '../../api/wechat'
  import {search, hotSearch} from '../../api'

  const KEY_HISTORY_SEARCH = 'historySearch'

  export default {
    name: 'search',
    components: {
      SearchBar,
      TagGroup,
      SearchList
    },
    computed: {
      showList() {
        const keys = Object.keys(this.searchList)
        return keys.length > 0
      },
      hotSearchArray() {
        const _hotSearch = []
        this.hotSearch.forEach(o => _hotSearch.push(o.title))
        return _hotSearch
      }
    },
    data() {
      return {
        hotSearch: [],
        hotSearchKeyWord: '',
        historySearch: [],
        searchList: {},
        searchFocus: true,
        openId: '',
        page: 1
      }
    },
    methods: {
      onConfirm(keyword) {
        if (!keyword || keyword.trim().length === 0) {
          keyword = this.hotSearchKeyWord
          this.$refs.searchBar.setValue(keyword)
        } else {
        }
        this.onSearch(keyword)
        if (!this.historySearch.includes(keyword)) {
          this.historySearch.push(keyword)
          setStorageSync(KEY_HISTORY_SEARCH, this.historySearch)
        }
        this.searchFocus = false
      },
      onClear() {
        this.searchList = {}
      },
      onChange(keyword) {
        if (!keyword || keyword.trim().length === 0) {
          this.searchList = {}
          return
        }
        this.page = 1
        this.onSearch(keyword)
      },
      onSearch(keyword) {
        search({
          keyword,
          openId: this.openId,
          page: this.page
        }).then(response => {
          console.log(response)
          this.searchList = response.data.data
        })
      },
      changeHotSearch() {
        hotSearch().then(response => {
          console.log(response)
          const {data: {data}} = response
          this.hotSearch = data
        })
      },
      showBookDetail(text, index) {
        console.log('show book detail...', text, index)
      },
      clearHistorySearch() {
        console.log('clear history search...')
        this.historySearch = []
        setStorageSync(KEY_HISTORY_SEARCH, [])
      },
      searchKeyWord(text) {
        this.$refs.searchBar.setValue(text)
        this.onSearch(text)
      }
    },
    mounted() {
      this.openId = getStorageSync('openId')
      hotSearch().then(response => {
        console.log(response)
        const {data: {data}} = response
        this.hotSearch = data
      })
      this.page = 1
      this.hotSearchKeyWord = this.$route.query.hotSearch
      this.historySearch = getStorageSync(KEY_HISTORY_SEARCH) || []
    },
    onPageScroll() {
      if (this.searchFocus) {
        this.searchFocus = false
      }
    },
    onReachBottom() {
      if (this.showList) {
        this.page++
        const searchword = this.$refs.searchBar.getValue()
        search({
          keyword: searchword,
          openId: this.openId,
          page: this.page
        }).then(response => {
          console.log(response)
          const { book } = response.data.data
          if (book && book.length > 0) {
            this.searchList.book.push(...book)
          } else {
            showToast('我是有底线的')
          }
        })
      }
    }
  }
</script>

<style scoped>

</style>
