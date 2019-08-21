<template>
  <div class="home">
    <SearchBar
      :disabled="true"
      @onClick="onSearchaBarClick"
    >//  等价于直接写  disable
    </SearchBar>
    <ImageView
      src="https://www.youbaobao.xyz/mpvue-res/big.jpg"
      round
      mode="scaleToFill"
      height="200px"
    >      //高度自适应的写法  height="300px" mode="scaleToFill"
    </ImageView>
  </div>
</template>

<script>
  import SearchBar from '../../components/home/SearchBar'
  import ImageView from '../../components/base/ImageView'

  export default {
    components: {
      SearchBar,
      ImageView
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
