<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
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
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script>
import Head from './components/header/header'

const ERR_OK = 0
export default {
  data () {
    return {
      seller: {
        id: 123
      }
    }
  },
  created () {
    this.$http.get('/api/seller')
      .then(res => {
        if (res.data.errno === ERR_OK) {
          this.seller = Object.assign({}, this.seller, res.data.data)
        }
      })
  },
  name: 'app',
  components: {
    'v-header': Head
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
  #app
    .tab
      display:flex
      width:100%
      height: 40px
      line-height 40px
      border-1px(rgba(7,17,27,0.1))
      .tab-item
        flex 1
        text-align center
        & > a
          display block
          font-size 14px
          color rgb(88,85,93)
          &.active
            color red

</style>
