<template>
  <div class="supports-bulletin">
    <div class="gray-mask">
      <div class="content">
        <div class="seller-name">{{seller.name}}</div>
        <star :score="seller.score" :itemClass="'star48'"></star>
        <div class="item-wrapper">
          <div class="title-wrapper">
            <span class="line"></span>
            <span class="title">优惠信息</span>
            <span class="line"></span>
          </div>
          <ul class="supports">
            <li v-for="(support,index) in seller.supports" :key="index">
              <span class="icon" :class="classMap[support.type]"></span>
              <span>{{support.description}}</span>
            </li>
          </ul>
        </div>
        <div class="item-wrapper">
          <div class="title-wrapper">
            <span class="line"></span>
            <span class="title">商家公告</span>
            <span class="line"></span>
          </div>
          <div class="bulletin">{{seller.bulletin}}</div>
        </div>
        <div class="close-wrapper" @click="showMask">
          <span class="icon-close"></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import star from './star'
export default {
  props: {
    seller:{
      type:Object
    },
    showMask:{
      type:Function
    }
  },
  created() {
    this.classMap = ['decrease','discount','special','invoice','guarantee'];
  },
  components:{
    star
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus" scoped>
@import '../assets/stylus/index.styl'
.supports-bulletin
  .gray-mask
    position fixed
    top 0
    right 0
    bottom 0
    left 0
    z-index 30
    margin auto
    width 100%
    height 100%
    background rgba(7,17,27,.9)
    .content
      width 100%
      height 100%
      color #fff
      .seller-name
        margin 34px 0 16px;
        text-align center
        font-size 16px
        font-weight 700
    .item-wrapper
      padding 28px 26px 0
      font-size 12px
      font-weight 200
      .title-wrapper
        display flex
        align-items center
        margin-bottom 24px
        .title
          padding 0 12px
          font-size 14px
          font-weight 700
        .line
          flex 1
          height 2px
          background rgba(255,255,255,.2)
      .supports
        li
          &:nth-child(n+2)
            margin-top 12px
          .icon
            display inline-block
            vertical-align top
            width 16px
            height 16px
            background-size 16px 16px
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.special
              bg-image('special_1')
            &.invoice
              bg-image('invoice_1')
            &.guarantee
              bg-image('guarantee_1')
      .bulletin
        margin-top:-12px
        line-height 24px
    .close-wrapper
      position absolute
      left 50%
      bottom 32px
      margin-left -16px
      .icon-close
        font-size 32px
        color rgba(255,255,255,.5)
</style>
