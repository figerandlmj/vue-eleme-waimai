<template>
<div class="food-detail">
  <div class="food-img">
    <img :src="food.image" alt="">
    <span class="icon-arrow_lift" @click="goDetail({})"></span>
  </div>
  <div class="food-content">
    <div class="title">{{food.name}}</div>
    <div class="sell-rating">
      <span class="sellCount">月售{{food.sellCount}}份</span>
      <span>好评率{{food.rating}}%</span>
    </div>
    <div class="content">
      <div class="price-wrapper">
        <span class="price">￥{{food.price}}</span>
        <span class="oldPrice">￥{{food.oldPrice}}</span>
      </div>
      <div class="add-shopcart">
        <span v-show="!food.count || food.count == 0" class="add-cart" @click="addCart">加入购物车</span>
        <cartcontrol v-show="food.count && food.count > 0" :food="food"></cartcontrol>
      </div>
    </div>
  </div>
  <div class="item-wrapper">
    <div class="title">商品介绍</div>
    <div class="info">{{food.info}}</div>
  </div>
  <filterRating :ratingFlag="'food'" :tags="tags" :current="current" :ratings="ratings"></filterRating>
</div>
</template>

<script>
import cartcontrol from './cartcontrol'
import filterRating from './filterRating'
import Vue from 'vue'
export default {
  name:'foodDetail',
  data () {
    return {
      ratings:[],
      tags: {'全部':-1,'推荐':1,'吐槽':0},
      current: {type:'全部',text:false}
    }
  },
  props:{
    food:{
      type:Object
    },
    goDetail:{
      type:Function
    }
  },
  methods:{
    addCart(){
      if(!this.food.count){
        Vue.set(this.food, "count");
        this.food.count = 1;
      }else{
        this.food.count ++;
      }
    }
  },
  created(){
    this.ratings = this.food.ratings;
  },
  components:{
    cartcontrol,
    filterRating
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus">
@import '../../static/style.css';
.food-detail
  position fixed
  top 0
  bottom 48px
  left 0
  z-index 10
  width 100%
  height 100%
  overflow auto
  background #f3f5f7
  .food-img
    position relative
    img
      width 100%
    .icon-arrow_lift
      position absolute
      top 18px
      left 18px
      color #fff
  .food-content
    padding 18px
    background #fff
    .title
      font-size 14px
      font-weight 700
      color rgb(7,17,27)
    .sell-rating
      margin 8px 0 10px
      font-size 10px
      color rgb(147,153,159)
      .cellCount
        margin-right 12px
  .content
    display flex
    .price-wrapper
      flex 1
      line-height 28px
      font-size 10px
      font-weight 700
      color rgb(147,153,159)
      .price
        margin-right 10px
        font-size 14px
        color rgb(240,20,20)
      .oldPrice
        text-decoration line-through
    .add-shopcart
      align-self center
      .add-cart
        display inline-block
        padding 8px 14px
        text-align center
        border-radius 20px
        font-size 10px
        color #fff
        background rgb(0,160,220)
  .item-wrapper
    margin-top 16px
    border-top 1px solid rgba(7,17,27,.1)
    border-bottom 1px solid rgba(7,17,27,.1)
    background #fff
    .title
      padding 18px 18px 0
      margin-bottom 6px
      font-size 14px
      color rgb(7,17,27)
  .info
    padding 0 18px 18px
    line-height 24px
    font-size 12px
    font-weight 200
    color rgb(147,153,159)
</style>
