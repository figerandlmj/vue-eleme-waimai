<template>
  <div class="shopcar">
    <div class="content">
      <div class="chart-icon-wrapper">
        <div class="chart-icon icon-shopping_cart" :class="{noChart: totalCount != 0}"></div>
        <div class="total-count" v-show="totalCount != 0">{{totalCount}}</div>
      </div>
      <div class="deliver-fee">
        <div class="price border-1px-right" :class="{noPrice: totalPrice != 0}">￥{{totalPrice}}</div>
        <div class="delivery-price">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="deliver-base" :class="{ok: this.totalPrice >= this.minPrice}">{{inform}}</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'shopcar',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  computed:{
    totalCount(){
      let totalCount = 0;
      return totalCount;
    },
    totalPrice(){
      let totalPrice = 0;
      return totalPrice;
    },
    inform(){
      if(this.totalPrice === 0){
        return `￥${this.minPrice}`;
      }else if(this.totalPrice > 0 && this.totalPrice < this.minPrice){
        return `还差￥${this.minPrice - this.totalPrice}起送`;
      }else{
        return `去结算`;
      }
    }
  },
  props:{
    deliveryPrice:{
      type:Number
    },
    minPrice:{
      type: Number
    }
  },
  created(){
    axios.get('/good/seller').then(
      res => {
        if(res.data.code === 0) {
          console.log(res.data.data);
        }
      }
    )
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus">
@import '../assets/stylus/index.styl'
.shopcar
  position fixed
  width 100%
  height 48px
  bottom 0
  left 0
  .content
    width 100%
    display flex
    background #141d27
    .chart-icon-wrapper
      flex 0 0 80px
      position relative
      .chart-icon
        position relative
        width 44px
        height 44px
        border-radius 44px
        border 6px solid #141d27
        background #2b333b
        margin-left 18px
        margin-top -10px
        font-size 24px
        color rgba(255,255,255,0.4)
        line-height 44px
        text-align center
        &.noChart
          background #00a0dc
          color #fff
      .total-count
        position absolute
        right 0
        top -6px
        text-align center
        background red
        color #fff
        width 24px
        height 16px
        font-size 8px 
        font-weight 700
        line-height 16px
        text-show 0 4px 8px 0 rgba(0,0,0,0.4)
        border-radius 16px
    .deliver-fee
      flex 1
      padding 12px 0 12px 12px
      height 24px
      .price
        display inline-block
        line-height 24px
        color rgba(255,255,255,0.2)
        border-1px-right(rgba(255,255,255,0.4))
        padding-right 12px
        &.noPrice
          color #fff
      .delivery-price
        display inline-block
        padding-left 12px
        font-size 12px
        color rgba(255,255,255,0.4)
        line-height 20px
        font-weight 700
    .deliver-base
      flex 0 0 105px
      padding 0 8px
      line-height 48px
      font-size 12px
      text-align center
      color rgba(255,255,255,0.1)
      font-weight 700
      background #2b333b
      &.ok
        background green
        color #fff
  
</style>
