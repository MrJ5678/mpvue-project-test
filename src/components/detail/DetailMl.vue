<template>
  <div class="detail-contents-wrapper">
    <div class="detail-contents-title">目录</div>
    <div
      class="detail-contents"
      v-for="(item, index) in contents"
      :key="index"
      @click="() => readBook(item.href)"
    >
      <div
        class="detail-contents-label"
        :style="{marginLeft: (15 * item.level) + 'px'}"
      >
        {{item.label}}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      contents: Array
    },
    methods: {
      readBook(nav) {
        this.$emit('readBook', nav)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .detail-contents-wrapper {
    padding: 0 0 60px 15px;
    margin-top: 15px;

  .detail-contents-title {
    font-size: 22px;
    color: #333333;
  }

  .detail-contents {
    padding: 20px 15px 20px 0;
    border-bottom: 1px solid #EBEBEB;

  &:last-child {
     border-bottom: none;
   }

  .detail-contents-label {
    font-size: 15px;
    color: #868686;
    line-height: 18px;
    max-height: 18px;
    text-overflow: ellipsis;
    overflow: hidden;
  }
  }
  }
</style>
