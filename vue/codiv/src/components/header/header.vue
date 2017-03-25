<template>
  <div id="header">
    <div class="header-wrapper">
      <div class="avatar"><img :src="seller.avatar" height="64" width="64"></div>
      <div class="header-info">
        <div class="title">
          <span class="icon"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description-wrapper">
          <span class="description">{{seller.description}}</span> /
          <span class="time">{{seller.deliveryTime}}</span>分钟送达
        </div>
        <div class="supports" v-if="seller.supports">
          <span class="icon" :class="classMain[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
    </div>
    <div class="detail-wrapper"></div>
  </div>

</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      seller: {}
    },
    created () {
      this.classMain = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    }
  }

</script>

<style lang="stylus" rel="stylesheet/stylus">
  #header
    background-color:#000
    color:#FFF
    font-size:0
    .header-wrapper
      padding:24px 12px 18px 24px
      .avatar
        display:inline-block
        vertical-align:top
        img
          border-radius:2px
      .header-info
        display:inline-block
        margin-left:16px
        .title
          font-size:16px
          line-height:18px


</style>
