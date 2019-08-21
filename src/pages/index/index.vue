<template>
  <div class="home">
    <SearchBar
      :disabled="true"
      @onClick="onSearchaBarClick"
    >//  等价于直接写  disable
    </SearchBar>
    <HomeCard></HomeCard>
  </div>
</template>

<script>
  import SearchBar from '../../components/home/SearchBar'
  import HomeCard from '../../components/home/HomeCard'

  export default {
    components: {
      SearchBar,
      HomeCard
    },
    methods: {
      onSearchaBarClick() {
        //  跳转到搜索页面

      }
    }
  }
</script>

<style lang="scss" scoped>

</style>
