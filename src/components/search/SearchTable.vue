<template>
    <div class="search-table-wrapper">
      <div class="search-table-inner">
        <div class="search-table-book"
             v-for="(book, index) in data"
             :key="index"
             @click="onClick(book)"
        >
          <div class="book-img-wrapper">
            <div class="book-img">
              <ImageView
                :src="book.cover"
              >
              </ImageView>
            </div>
          </div>
          <div class="book-info-wrapper">
            <div class="book-title">{{book.title}}</div>
            <div class="book-author">{{book.author}}</div>
            <div class="book-category">{{book.categoryText}}</div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
  import ImageView from '../base/ImageView'

  export default {
    name: 'SearchTable',
    components: {
      ImageView
    },
    props: {
      data: Array
    },
    methods: {
      onClick(book) {
        this.$emit('onClick', book)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .search-table-wrapper {
    padding: 0 16px;
    .search-table-inner {
      .search-table-book {
        margin: 14.5px 0;
        display: flex;
        align-items: center;
        .book-img-wrapper {
          .book-img {
            width: 47px;
            height: 68.5px;
          }
        }
        .book-info-wrapper {
          margin-left: 15.5px;
          width: 80%;
          .book-title {
            width: 100%;
            font-size: 16px;
            line-height: 22.5px;
            color: #333333;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            font-weight: 500;
          }
          .book-author {
            margin-top: 5px;
            font-size: 13px;
            color: rgba(0,0,0,.65);
            line-height: 18px;
          }
          .book-category {
            font-size: 13px;
            color: rgba(0,0,0,.45);
            line-height: 18px;
          }
        }
      }
    }
  }
</style>
