<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <ul class="tab-wrapper">
        <li class="tab-item"><router-link to="/goods">商品</router-link></li>
        <li class="tab-item"><router-link to="/seller">评价</router-link></li>
        <li class="tab-item"><router-link to="/ratings">商家</router-link></li>
      </ul>
    </div>
    <router-view></router-view>
  </div>

</template>

<!--suppress JSUnresolvedVariable -->
<script type="text/ecmascript-6">
import header from './components/header/header'
let ERR_OK = 0

export default {
  data () {
    return {
      seller : {}
    }
  },
  created () {
    this.$http.get('api/seller').then(response => {
      const res = response.body
      if (res.errno === ERR_OK) {
        this.seller = res.data
      }
    })
  },
  components: {
    'v-header': header
  }
}
</script>

<style  lang="stylus" rel="stylesheet/stylus">

.tab
  height:40px
  position:relative
  .tab-wrapper
    display:flex
  .tab-item
    flex:1
    text-align:center





</style>
