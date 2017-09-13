<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="header"></div>
    <div class="tab border-1px">
      <div class="tab-item">
        <!--点击绑定路由组件-->
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <!--添加路由组件显示不同区域的信息-->
    <router-view></router-view>
  </div>
</template>
<script type="text/ecmascript-6">
    const ERR_OK = 0
    import header from './components/header/header.vue'
    export default {
      data () {
        return {
          seller: {}
        }
      },
      created () {
        // 获取数据 vue-resource提供的方法
        this.$http.get('/api/seller').then((response) => {
          response = response.body
          if (response.errno === ERR_OK) {
            this.seller = response.data
            console.log(this.seller)
          }
        })
      },
      components: {
        'v-header': header
      }
    }
</script>
<!--设计按钮样式-->
<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
    #app 
      .tab
        display : flex
        width: 100%
        height: 40px
        line-height: 40px
        //border-bottom 0.5px solid rgba(7,17,27,0.1)
        border-1px(rgba(7,17,27,0.1))
        .tab-item
            flex: 1
            text-align: center
            & > a
              display: block
              font-size: 14px
              color: rgb(77,85,93)
              line-height: 28px
              &.active
                color rgb(240,20,20)      
</style>