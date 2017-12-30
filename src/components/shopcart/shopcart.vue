<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highLight':totalCount>0}">
            <i class="icon-shopping_cart" :class="{'highLight':totalCount>0}"></i>
          </div>
          <div class="num" v-show="totalCount>0">{{totalCount}}</div>
        </div>
        <div class="shopcart-price" :class="{'highLight':totalPrice>0}">${{totalPrice}}元</div>
        <div class="shopcart-desc">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="content-right">
        <div class="pay" :class="payClass">{{payDesc}}</div>
      </div>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">
  export default {
    props: {
      deliveryPrice: {},
      minPrice: {},
      selectFoods: {
        type: Array,
        default() {
          return [
            {
              price: 30,
              count: 1
            }
          ]
        }
      }
    },
    computed: {
      // 总价格
      totalPrice() {
        let total = 0
        this.selectFoods.forEach((food) => {
          total += food.price * food.count
        })
        return total
      },
      // 总数量
      totalCount() {
        let count = 0
        this.selectFoods.forEach((food) => {
          count += food.count
        })
        return count
      },
      // 配送 描述
      payDesc() {
        if (this.totalPrice === 0) {
          return `￥${this.minPrice}元起送`
        } else if (this.totalPrice < this.minPrice) {
          let diff = this.minPrice - this.totalPrice
          return `还差￥${diff}元起送`
        } else {
          return `去结算`
        }
      },
      // 配送 价格差异 样式切换
      payClass() {
        if (this.totalPrice < this.minPrice) {
          return 'not-enough'
        } else {
          return 'enough'
        }
      }
    },
    methods: { }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shopcart
    position:fixed
    bottom:0
    left: 0
    width: 100%
    height: 48px
    background:#141d27
    .content
      display:flex
      font-size:0
      color: rgba(255, 255, 255, 0.4)
      .content-left
        flex:1
        .logo-wrapper
          position:relative
          display:inline-block
          vertical-align:top
          width: 56px
          height:56px
          border-radius:50%
          box-sizing: border-box
          top:-10px
          background:#141d27
          margin: 0 8px
          padding:6px
          .logo
            width: 100%
            height:100%
            background:#2b343c
            border-radius:50%
            text-align:center
            &.highLight
              background:rgb(0,160,220)
            .icon-shopping_cart
              font-size:24px
              line-height: 44px
              color: #80858a
              &.highLight
                color:#fff
          .num
            position:absolute
            top: 0
            right: 0
            width: 24px
            height:16px
            font-size:9px
            line-heihgt:16px
            text-align:center
            background:rgb(240,20,20)
            border-radius:16px
            box-shadow:0 4px 8px 0 rgba(0,0,0,.4)
            color:white

        .shopcart-price
          display: inline-block
          vertical-align: top
          margin-top: 12px
          line-height: 24px
          padding-right:6px
          box-sizing: border-box
          border-right: 1px solid rgba(255, 255, 255, 0.1)
          font-size: 16px
          font-weight: 700
          &.highLight
            color:#fff
        .shopcart-desc
          display: inline-block
          vertical-align: top
          line-height: 24px
          font-size: 10px
          margin-top:12px
          padding-left:6px
      .content-right
        flex:0 0 105px
        width:105px
        background-color: #2b333b
        .pay
          height: 48px
          line-height: 48px
          text-align: center
          font-size: 12px
          font-weight: 700
          &.not-enough
            background: #2b333b
          &.enough
            background: #00b43c
            color:#fff
</style>