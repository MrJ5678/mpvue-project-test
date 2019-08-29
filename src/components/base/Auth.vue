<template>
  <div class="auth-wrapper">
    <div class="auth">
      <div class="auth-info">
        <div class="auth-img">
          <ImageView
            round
            src="https://www.youbaobao.xyz/mpvue-res/logo.jpg"
            height="100%"
            mode="scaleToFill"
          >
          </ImageView>
        </div>
        <div class="sub-title">登录小慕读书</div>
        <div class="title">全网好书免费阅读</div>
      </div>
      <button
        class="auth-btn"
        open-type="getUserInfo"
        @getuserinfo="getUserInfo"
      >
        授权登录
      </button>
    </div>
  </div>
</template>

<script>
  import ImageView from './ImageView'
  export default {
    name: 'Auth',
    components: {
      ImageView
    },
    methods: {
      getUserInfo() {
        this.$emit('getUserInfo')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .auth-wrapper {
    position: fixed;
    left: 0;
    top: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background: #999;
    z-index: 1000;
    .auth {
      position: relative;
      width: 270px;
      height: 248px;
      background: #F5F5F5;
      border-radius: 18px;
      .auth-info {
        margin-top: 22.5px;
        display: flex;
        flex-direction: column;
        align-items: center;
        .auth-img {
          height: 74px;
          width: 74px;
        }
        .sub-title {
          margin-top: 18px;
          font-family: PingFangSC-Regular;
          font-size: 13px;
          line-height: 18.5px;
          color: #999;
        }
        .title {
          margin-top: 3.5px;
          font-family: PingFangSC-Regular;
          font-size: 16px;
          line-height: 22.5px;
          font-weight: bold;
          color: #333;
        }
      }
      .auth-btn {
        position: absolute;
        bottom: 0;
        width: 100%;
        background-image: linear-gradient(90deg, #1EA3F5 0%, #0F87FC 100%);
        border-radius: 0 0 18px 18px;
        font-size: 15px;
        line-height: 49px;
        color: #FFFFFF;
        height: 49px;
      }
    }
  }
</style>
