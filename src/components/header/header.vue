<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" width="64" height="64">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <div class="text">{{seller.supports[0].description}}</div>
        </div>
      </div>
      <div class="supports-count" v-if="seller.supports" @click="show">
        <span class="count">{{seller.supports.length}}个</span>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="show">
      <span class="bulletin"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="backgroud">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="showDetail" class="showDetail" translate="fade">
      <div class="detail-wrapper">
        <div class="detail-main">
          <h1 class="seller-name">{{seller.name}}</h1>
          <div class="star-wrapper">
            <star class="" :size="48" :score="seller.score"></star>
          </div>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul class="supports" v-if="seller.supports">
            <li class="supports-item" v-for="(item,index) in seller.supports">
              <span class="supports-icon" :class="classMap[index]"></span>
              <span class="supports-text">{{item.description}}</span>
            </li>
          </ul>
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <div class="bulletin-detail">
            <p class="content">{{seller.bulletin}}</p>
          </div>
        </div>
      </div>
      <div class="detail-footer" @click="hide">
        <i class="icon-close"></i>
      </div>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
  import star from '../star/star'
  export default {
    props: {
      seller: {
      }
    },
    data() {
      return {
        showDetail: false
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    },
    methods: {
      show() {
        this.showDetail = true
      },
      hide() {
        this.showDetail = false
      }
    },
    components: {
      'star': star
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin"
  .header
    position:relative
    color: #fff
    background:rgba(7,17,27,.5)
    overflow:hidden
    .content-wrapper
      padding:24px 16px 18px 24px
      vertical-align: top
      font-size:0
      .avatar
        display:inline-block
        vertical-align :top
      .content
        display:inline-block
        font-size:14px
        margin-left:16px
        .title
          .brand
            width: 30px
            height:18px
            display :inline-block
            background-size: 30px 18px
            background-repeat:no-repeat
            vertical-align :top
            margin:2px 6px 8px 0
            bg-image(brand)
          .name
            line-height: 18px
            font-size:14px
            font-weight :bold
            color:rgb(255,255,255)
        .description
          font-size: 12px
          font-weight: 200
          line-height: 12px
          color:rgb(255,255,255)
          margin-bottom:10px
        .supports
          .icon
            margin-right:4px
            width: 12px
            height:12px
            background-repeat:no-repeat
            background-size:12px 12px
            display :inline-block
            vertical-align: top
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            display :inline-block
            font-size: 10px
            line-height:12px
            color:rgb(255,255,255)
      .supports-count
        padding:4px
        width: 45px
        border-radius:14px
        position:absolute
        right: 10px
        top:70px
        font-size:10px
        line-height:20px
        text-align :center
        background: rgba(0, 0, 0, 0.2)
        .count
          font-size:10px
          display:inline-block
          vertical-align :top
        .icon-keyboard_arrow_right
          /*display :inline-block*/
          margin-right: 2px
          font-size: 10px

    .bulletin-wrapper
      position:relative
      height: 28px
      background:rgba(7,17,27,.2)
      line-height:28px
      white-space: nowrap
      overflow: hidden
      text-overflow: ellipsis

      .bulletin
        vertical-align:top
        width: 22px
        height: 12px
        display:inline-block
        background-repeat:no-repeat
        background-size:22px 12px
        bg-image('bulletin')
        margin:8px 4px 8px 12px
      .bulletin-text

        font-size:10px
        font-weight: 200
        line-height: 28px
        margin-right:2px
      .icon-keyboard_arrow_right
        position:absolute
        top: 8px
        right:-1px
    .backgroud
      position: absolute
      left:0
      top: 0
      width: 100%
      heihgt:100%
      z-index:-1
      filter:blur(10px)
    .showDetail
      overflow:auto
      z-index:999
      width: 100%
      height:100%
      position:fixed
      top: 0
      left: 0
      background:rgba(7,17,27,.8)
      transition:all 0.5s
      backdrop-filter: blur(10px)
      .detail-wrapper
        width:100%
        min-height:100%
        text-align:center
        .detail-main
          padding-bottom:32px
          padding-top: 64px;
          .seller-name
            line-height: 16px
            font-size:16px
            font-weight: 700
            color:rgb(255,255,255)
          .star-wrapper
            margin-top: 18px
            margin-bottom:18px
            padding: 2px 0
            text-align: center
          .title
            display:flex
            justify-content:center
            .line
              flex:1
              width:112px
              height:auto
              border-top:1px solid rgba(255,255,255,.2)
              margin:7.5px 12px 7.5px 16px
            .text
              font-size:14px
              line-height:14px
          .supports
            margin:24px auto
            text-align:left
            width:80%
            .supports-item
              margin-bottom:12px
              height:16px
              .supports-icon
                vertical-align:top
                display:inline-block
                width: 16px
                height: 16px
                background-size:16px 16px
                background-repeat:no-repeat
                &.decrease
                  bg-image('decrease_2')
                &.discount
                  bg-image('discount_2')
                &.guarantee
                  bg-image('guarantee_2')
                &.invoice
                  bg-image('invoice_2')
                &.special
                  bg-image('special_2')
              .supports-text
                display:inline-block
                font-size: 12px
                line-height: 16px
                margin-left:6px
          .bulletin-detail
            width: 80%
            margin:24px auto auto auto
            .content
              font-size: 12px
              line-height:24px
              color:rgb(255,255,255)
              font-weight:200
              text-align:left
              padding:0 12px
      .detail-footer
        width: 32px
        height: 32px
        margin:-32px auto
        font-size: 32px
        .icon-close
          font-size:32px
          color:rgba(255,255,255,.5)
</style>
