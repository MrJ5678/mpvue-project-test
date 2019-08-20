<template>
  <div class="home">
    <SearchBar
      :disabled="true"
      @onClick="onSearchaBarClick"
    >//  等价于直接写  disable
    </SearchBar>
  </div>
</template>

<script>
  import SearchBar from '../../components/home/SearchBar'

  export default {
    components: {
      SearchBar
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
