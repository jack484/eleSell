<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo">
            <i class="icon-shopping_cart"></i>
          </div>
        </div>
        <div class="price"></div>
        <div class="desc"></div>
      </div>
      <div class="content-right"></div>
    </div>
  </div>
</template>
<script type="text/ecmascript-6">

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
          margin: 0 12px
          padding:6px
          .logo
            width: 100%
            height:100%
            background:#2b343c
            border-radius:50%
            text-align:center
            .icon-shopping_cart
              font-size:24px
              line-height: 44px
              color: #80858a

      .content-right
        flex:0 0 110px
</style>