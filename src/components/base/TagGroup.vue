<template>
  <div class="tag-group-wrapper">
    <div class="tag-group-header">
      <div class="header-text">{{headerText}}</div>
      <div class="header-btn"
           @click="onBtnClick"
      >
        {{btnText}}
      </div>
    </div>
    <div class="tag-group">
      <div
        class="tag-group-inner"
        v-for="(text, index) in value"
        :key="index"
      >
        <Tag
          :text="text"
          @onClick="onTagClick(text, index)"
        >
        </Tag>
      </div>
    </div>
  </div>
</template>

<script>
  import Tag from './Tag'

  export default {
    name: 'TagGroup',
    components: {
      Tag
    },
    props: {
      headerText: String,
      btnText: String,
      value: Array
    },
    methods: {
      onTagClick(text, index) {
        this.$emit('onTagClick', text, index)
      },
      onBtnClick() {
        this.$emit('onBtnClick')
      }
    }
  }
</script>

<style lang="scss" scoped>
  .tag-group-wrapper {
    width: 100%;
    margin-top: 35px;
    padding-bottom: 10px;
    .tag-group-header {
      padding: 0 16px;
      display: flex;
      justify-content: space-between;
      font-size: 14px;
      line-height: 20px;
      .header-text {
        color: #333;
      }
      .header-btn {
        color: #3696EF;
      }
    }
    .tag-group {
      width: 100%;
      box-sizing: border-box;
      display: flex;
      flex-flow: row wrap;
      padding: 4px 10px 0 10px;
      .tag-group-inner {
        max-width: 100%;
        box-sizing: border-box;
        padding: 12px 6px 0 6px;
      }
    }
  }
</style>
