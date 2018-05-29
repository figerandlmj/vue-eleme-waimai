<template>
  <div class="shopcar">
    <div class="content">
      <div class="chart-icon-wrapper" @click="changeShow">
        <div class="chart-icon icon-shopping_cart" :class="{noChart: totalCount != 0}"></div>
        <div class="total-count" v-show="totalCount != 0">{{totalCount}}</div>
      </div>
      <div class="deliver-fee">
        <div class="price border-1px-right" :class="{noPrice: totalPrice != 0}">￥{{totalPrice}}</div>
        <div class="delivery-price">另需配送费￥{{deliveryPrice}}</div>
      </div>
      <div class="deliver-base" :class="{ok: this.totalPrice >= this.minPrice}">{{inform}}</div>
    </div>
    <div class="car-list-wrapper" v-show="showList">
      <div class="car-gray" @click="changeShow"></div>
      <div class="car-list">
        <div class="car-list-header">
          <span class="car-title">购物车</span>
          <span class="clear" @click="clear">清空</span>
        </div>
        <div class="food-item" v-for="food in selectFoods" :key="food.id">
          <span class="food-title">{{food.name}}</span>
          <span class="food-price">￥{{food.price}}</span>
          <cartcontrol class="cart-control" :food="food"></cartcontrol>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import cartcontrol from './cartcontrol'
import Vue from 'vue'

export default {
  name: 'shopcar',
  data () {
    return {
      fold: true
    }
  },
  methods:{
    changeShow(){
      this.fold = !this.fold;
    },
    clear(){
      this.selectFoods.forEach(food => {
        Vue.set(food, "count");
      });
    }
  },
  computed:{
    totalCount(){
      let totalCount = 0;
      this.selectFoods.forEach((food) => {
        totalCount += food.count;
      })
      return totalCount;
    },
    totalPrice(){
      let totalPrice = 0;
      this.selectFoods.forEach((food) => {
        totalPrice += food.price * food.count;
      })
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
    },
    showList(){
      if(!this.totalCount){
        this.fold = true
        return false
      }
      return !this.fold;
    }
  },
  props:{
    deliveryPrice:{
      type:Number
    },
    minPrice:{
      type: Number
    },
    selectFoods:{
      type:Array,
      default(){
        return [];
      }
    }
  },
  created(){
    // axios.get('/good/seller').then(
    //   res => {
    //     if(res.data.code === 0) {
    //       console.log(res.data.data);
    //     }
    //   }
    // )
  },
  components:{
    cartcontrol
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus">
@import '../assets/stylus/index.styl'
::-webkit-scrollbar
  display:none
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
      flex 0 0 70px
      position relative
      .chart-icon
        position relative
        width 44px
        height 44px
        border-radius 44px
        border 6px solid #141d27
        background #2b333b
        margin-left 8px
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
        right 10px
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
      flex 3
      display flex
      padding 12px 0 12px 0
      height 24px
      .price
        display inline-block
        line-height 24px
        color rgba(255,255,255,0.2)
        border-1px-right(rgba(255,255,255,0.4))
        padding-right 10px
        &.noPrice
          color #fff
      .delivery-price
        display inline-block
        padding-left 10px
        font-size 12px
        color rgba(255,255,255,0.4)
        line-height 22px
        font-weight 700
    .deliver-base
      flex 2
      line-height 48px
      font-size 12px
      text-align center
      color rgba(255,255,255,0.1)
      font-weight 700
      background #2b333b
      &.ok
        background green
        color #fff
  .car-list-wrapper
    position fixed
    top 0
    bottom 48px
    width 100%
    display flex
    flex-direction column
    z-index -1
    .car-gray
      flex 1
      background rgba(7,17,27,0.6)
    .car-list
      width 100%
      position fixed
      bottom 48px
      left 0
      background #fff
      max-height 217px
      overflow hidden
      overflow-y auto
      .car-list-header
        height 40px
        line-height 40px
        padding 0 18px
        border-1px(rgba(7,17,27,0.1))
        background #f3f5f7
        .car-title
          font-size 14px
          font-weight 200
          color rgb(7,17,27)
        .clear
          position absolute
          right 18px
          font-size 12px
          color rgb(0,160,220)
      .food-item
        width 100%
        height 48px
        line-height 48px
        margin 0 18px
        border-1px(rgba(7,17,27,0.1))
        .food-title
          font-size 14px
          color rgb(7,17,27)
        .food-price
          position absolute
          right 120px
          font-size 10px
          color rgb(240,20,20)
        .cart-control
          position absolute
          right 34px
          bottom 0
          display inline-block


</style>
