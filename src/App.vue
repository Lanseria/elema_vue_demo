<template>
  <div id="app">
    <vheader :seller="seller"></vheader>
    <div class="tab border-1px">
      <!-- 使用 router-link 组件来导航. -->
      <!-- 通过传入 `to` 属性指定链接. -->
      <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <keep-alive>
      <router-view :seller="seller" :bus="bus"></router-view>
    </keep-alive>
  </div>
</template>

<script type="text/ecmascript-6">
import Vue from 'vue'
import vheader from './components/header/header'

const ERR_OK = 0

export default {
  name: 'app',
  data () {
    return {
      seller: {},
      bus: new Vue()
    }
  },
  created () {
    this.$http.get('/api/seller').then((res) => {
      res = res.body
      if (res.errno === ERR_OK) {
        this.seller = res.data
        // console.log(this.seller)
      }
    })
  },
  components: {
    vheader
  }
}
</script>

<style lang="stylus" rel="stylesheet" scoped>
  @import "./common/stylus/mixin.styl"
   
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      // border-bottom: 1px solid rgba(7, 17, 27, 0.1)
      border-1px(rgba(7, 17, 27, 0.1))
      .tab-item
        flex: 1
        text-align: center
        & > a
          display: block
          font-size: 14px
          color: rgb(77, 85, 93)
          &.active
            color: rgb(240, 20, 20)
</style>
