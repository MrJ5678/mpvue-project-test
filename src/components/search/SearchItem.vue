<template>
  <div class="search-item-wrapper" @click="onClick">
    <div class="search-item-icon">
      <div class="icon-wrapper">
        <van-icon
          :name="icon"
          color="rgba(0, 0, 0, .5)"
          :style="{ width:'20px', height:'20px' }"
          size="20px"
        >
        </van-icon>
      </div>
    </div>
    <div class="search-icon-info">
      <div class="search-item-title">{{title}}</div>
      <div class="search-item-subtitle">{{subTitle}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'SearchItem',
    props: {
      title: String,
      subTitle: String,
      icon: String
    },
    methods: {
      onClick() {
        this.$emit('onClick')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .search-item-wrapper {
    display: flex;
    align-items: center;
    padding: 15px;
    height: 36.5px;
    .search-item-icon {
      .icon-wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 32px;
        height: 32px;
        background: #F7F7F9;
        border-radius: 50%;
      }
    }
    .search-icon-info {
      margin-left: 10px;
      width: 80%;
      .search-item-title{
        width: 100%;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        font-size: 14px;
        line-height: 20px;
        color: #333;
      }
      .search-item-subtitle {
        font-size: 12px;
        line-height: 16.5px;
        color: rgba(0,0,0,0.45);
      }
    }
  }
</style>
