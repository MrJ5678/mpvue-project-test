<template>
  <div class="home-card">
    <div class="home-card-inner">
      <div class="user-info">
        <div class="avatar-wrapper">
          <ImageView
            :src="avatar"
            round
            height="100%"
            mode="scaleToFill"
          >
          </ImageView>
        </div>
        <div class="nickname">{{ nickname }}</div>
        <div class="shelf-text">书架共有{{ data.num }}本好书</div>
        <div class="round-item"></div>
        <div class="shelf-text">特别精选</div>
      </div>
      <div class="book-info">
        <div class="book-wrapper">
          <div class="book-image-wrapper"
               v-for="(item,index) in bookList"
               :key='index'
               @click="onBookClick(item)"
          >
            <ImageView
              :src="item.cover"
            >
            </ImageView>
          </div>
        </div>
        <div class="shelf-wrapper">
          <div class="shelf">书架</div>
          <van-icon
            class="arrow"
            name="arrow"
            size="11px"
            color="#828489"
          >
          </van-icon>
        </div>
      </div>
      <div class="feedback-wrapper"></div>
      <div class="feedback-text" @click="onFeedBackClick">反馈</div>
    </div>
    <van-dialog id="van-dialog"></van-dialog>
  </div>
</template>

<script>
  import ImageView from '../base/ImageView'
  import Dialog from 'vant-weapp/dist/dialog/dialog'

  export default {
    name: 'HomeCard',
    components: {ImageView},
    props: {
      data: Object,
      hasSign: {
        type: Boolean,
        default: false
      },
      signDay: {
        type: Number,
        default: 0
      }
    },
    computed: {
      avatar() {
        return (this.data && this.data.userInfo && this.data.userInfo.avatarUrl) || ''
      },
      nickname() {
        return (this.data && this.data.userInfo && this.data.userInfo.nickName) || ''
      },
      bookList() {
        return (this.data && this.data.bookList) || []
      }
    },
    methods: {
      gotoShelf() {

      },
      onBookClick(item) {
        this.$emit('onClick', item)
      },
      sign() {

      },
      onFeedBackClick() {
        Dialog.confirm({
          title: '反馈',
          message: '您是否确认提交反馈信息？',
          confirmButtonText: '是',
          cancelButtonText: '否'
        }).then(() => {
          console.log('点击是之后的事件')
        }).catch(() => {
          console.log('点击否之后的事件')
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .home-card {
    background-image: linear-gradient(-90deg, #54575F 0%, #595B60 100%);
    border-radius: 15px;
    margin: 22px 20px 0;

    .home-card-inner {
      position: relative;
      padding: 22px 17px 20px 20px;
      box-sizing: border-box;

      .user-info {
        display: flex;
        align-items: center;

        .avatar-wrapper {
          width: 20px;
          height: 20px;
        }

        .nickname {
          font-family: PingFangSC-Regular;
          font-size: 12px;
          color: #FFF;
          margin: 0 8.5px;

        }

        .shelf-text {
          opacity: 0.7;
          font-family: PingFangSC-Regular;
          font-size: 12px;
          color: #FFFFFF;
        }

        .round-item {
          width: 4px;
          height: 4px;
          background: #A2A2A2;
          border-radius: 50%;
          margin: 0 8px;
        }
      }

      .book-info {
        display: flex;
        margin-top: 16.5px;

        .book-wrapper {
          flex: 1;
          display: flex;
          justify-content: space-around;

          .book-image-wrapper {
            width: 72px;
            height: 101px;
          }
        }

        .shelf-wrapper {
          display: flex;
          align-items: center;

          .shelf {
            font-size: 11px;
            width: 11px;
            word-break: break-word;
            opacity: .8;
            font-family: PingFangSC-Regular;
            color: #FFF;
          }
        }
      }

      .feedback-wrapper {
        position: absolute;
        right: 0;
        top: 19.5px;
        width: 44.5px;
        height: 23.5px;
        background: #d8d8d8;
        opacity: .3;
        border-radius: 100px 0 0 100px;
      }

      .feedback-text {
        position: absolute;
        right: 0;
        top: 19.5px;
        color: #fff;
        font-size: 11px;
        line-height: 23.5px;
        width: 44.5px;
        height: 23.5px;
        text-align: center;
      }
    }
  }
</style>
