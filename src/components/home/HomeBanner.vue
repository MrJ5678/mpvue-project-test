<template>
  <div class="home-banner" @click="onClick">
    <div
      class="bg-img"
      :style="{backgroundImage: bgImg}"
    >
      <div class="title">{{title}}</div>
      <div class="sub-title">{{subTitle}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HomeBanner',
    props: {
      title: String,
      subTitle: String,
      img: String
    },
    computed: {
      bgImg() {
        return 'url(' + this.img + ')'
      }
    },
    methods: {
      onClick() {
        this.$emit('onClick')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .home-banner {
    margin-top:20px;
    padding:0 20px;
    box-sizing:border-box;
    .bg-img {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 125px;
      border-radius:10px;
      background-size:100% 100%;
      background-repeat:no-repeat;
      .title {
        font-size: 18px;
        font-weight: 500;
        color:#fff;
      }
      .sub-title {
        padding:5px 15px;
        background:#4585ff;
        border:1px solid #ccc;
        border-radius: 50px;
        margin-top:10px;
        font-size: 14px;
        color:#fff;
      }
    }
  }
</style>
