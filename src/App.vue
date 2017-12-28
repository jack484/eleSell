<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <div class="content"></div>
    <router-view :seller="seller"  keep-alive></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header'
  export default {
    name: 'app',
    data () {
      return {
        goods: [],
        seller: [],
        ratings: []
      }
    },
    created () {
      this.$nextTick(() => {
        this.getDataJson()
      })
    },
    methods: {
      getDataJson () {
        this.$axios.get('./data.json').then((res) => {
          this.seller = res.data.seller
          this.goods = res.data.goods
          this.ratings = res.data.ratings
        })
      }
    },
    components: {
      'v-header': header
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "common/stylus/mixin.styl"
  #app
    .tab
      display: flex
      width:100%
      height:40px
      line-height:40px
      border-1px(rgba(7, 17, 27, 0.1))
      // border-bottom:1px solid rgba(7,17,27,0.1)
      .tab-item
        text-align:center
        flex:1
        & > a
          display :block
          color:rgb(77,85,93)
          font-size:14px
          &.router-link-active
            color: rgb(240,20,20)
</style>
