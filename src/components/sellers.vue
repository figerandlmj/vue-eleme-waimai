<template>
  <div class="sellers">
    <div class="basic-msg">
      <div class="top">
        <div class="left">
          <div class="title">{{seller.name}}</div>
          <div class="star-sell">
            <star :score="seller.score" :itemClass="'star36'" class="stars"></star>
            <span class="ratingCount">({{seller.ratingCount}})</span>
            <span>月售{{seller.sellCount}}单</span>
          </div>
        </div>
        <div class="right">
          <span class="icon icon-favorite" :class="{'active':seller.collection === 1}"></span>
          <span>{{seller.collection === 1 ? '已收藏' : '未收藏'}}</span>
        </div>
      </div>
      <div class="bottom">
        <div>
          <span class="tip">起送价</span>
          <span><i>{{seller.minPrice}}</i>元</span>
        </div>
        <div>
          <span class="tip">商家配送</span>
          <span><i>{{seller.deliveryPrice}}</i>元</span>
        </div>
        <div>
          <span class="tip">平均配送时间</span>
          <span><i>{{seller.deliveryTime}}</i>分钟</span>
        </div>
      </div>
    </div>
    <div class="bulletin-supports">
      <div class="top">
        <div class="title">公告与活动</div>
        <div class="bulletin">{{seller.bulletin}}</div>
      </div>
      <div class="bottom">
        <ul>
          <li v-for="item in seller.supports" :key="item.type">
            <span class="icon" :class="classMap[item.type]"></span>
            <span>{{item.description}}</span>
          </li>
        </ul>
      </div>
    </div>
    <div class="pics-wrapper">
      <div class="title">商家实景</div>
      <ul>
        <li v-for="(pic,index) in seller.pics" :key="index">
          <img :src="pic">
        </li>
      </ul>
    </div>
    <div class="infos-wrapper">
      <div class="title">商家信息</div>
      <ul>
        <li v-for="(info,index) in seller.infos" :key="index">
          {{info}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import star from './star'
export default {
  name: 'sellers',
  data () {
    return {
    }
  },
  props:{
    seller:{
      type:Object
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
<style lang="stylus" ref="stylesheet/stylus">
@import '../../static/style.css';
.sellers
  background #f3f5f7
  >div
    border-bottom 1px solid rgba(7,17,27,.1)
    background #fff
    &:nth-child(n+2)
      margin-top 18px
      border-top 1px solid rgba(7,17,27,.1)
  .top
    margin 0 18px
    border-bottom 1px solid rgba(7,17,27,.1)
  .title
    margin 18px 0 8px
    font-size 14px
    font-weight 600
    color rgb(7,17,27)
  .basic-msg
    .top
      display flex
      padding-bottom 18px
      font-size 10px
      color rgb(77,85,93)
    .left
      flex 1
      span
        display inline-block
        vertical-align middle
      .ratingCount
        margin 0 8px 0 4px
      .stars
        display inline-block
        vertical-align middle
    .right
      align-self flex-end
      text-align center
      .icon-favorite
        display block
        margin-bottom 6px
        font-size 24px
        color rgba(7,17,27,.2)
        &.active
          color rgb(240,20,20)
    .bottom
      display flex
      margin 18px
      >div
        flex 1
        &:nth-child(n+2)
          border-left 1px solid rgba(7,17,27,.1)
        text-align center
        font-size 10px
        font-weight 200
        color rgb(7,17,27)
      .tip
        display block
        margin-bottom 4px
        font-size 10px
        color rgb(147,153,159)
      i
        font-size 24px
  .bulletin-supports
    .bulletin
      padding 0 0 16px 12px
      line-height 24px
      font-size 12px
      font-weight 200
      color rgb(240,20,20)
    .bottom
      margin 0 18px
      font-size 12px
      font-weight 200
      li
        padding 16px 12px
        &:nth-child(n+2)
          border-top 1px solid rgba(7,17,27,.1)
        .icon
          display inline-block
          vertical-align middle
          width 16px
          height 16px
          background-size 16px 16px
          background-repeat:no-repeat
          &.decrease
            background-image:url("../assets/images/decrease_3@2x.png")
            // bg-image('decrease_3')
          &.discount
            background-image:url("../assets/images/discount_3@2x.png")
            // bg-image('discount_3')
          &.special
            background-image:url("../assets/images/special_3@2x.png")
            // bg-image('special_3')
          &.invoice
            background-image:url("../assets/images/invoice_3@2x.png")
            // bg-image('invoice_3')
          &.guarantee
            background-image:url("../assets/images/guarantee_3@2x.png")
            // bg-image('guarantee_3')
  .pics-wrapper
    padding 0 18px 18px
    overflow: hidden;
    ul
      overflow-x: scroll;
      white-space: nowrap;
    li
      display inline-block
      width 120px
      height 90px
      &:nth-child(n+2)
        margin-left 6px
      img
        width 100%
        height 100%
  .infos-wrapper
    padding 0 18px
    li
      padding 16px 12px
      border-top 1px solid rgba(7,17,27,.1)
      line-height 16px
      font-size 12px
      font-weight 200
      color rgb(7,17,27)



</style>
