<template>
<div class="seller-ratings">
  <div class="general-rating">
    <div class="left">
      <p class="score">{{seller.score}}</p>
      <p class="tip">综合评分</p>
      <p class="rankRate">高于周边商家{{seller.rankRate}}%</p>
    </div>
    <div class="right">
      <div class="star-rating">
        <span class="tip">服务态度</span>
        <star :score="seller.serviceScore" :itemClass="'star36'" class="stars"></star>
        <span class="score">{{seller.serviceScore}}</span>
      </div>
      <div class="star-rating">
        <span class="tip">商品评价</span>
        <star :score="seller.foodScore" :itemClass="'star36'" class="stars"></star>
        <span class="score">{{seller.foodScore}}</span>
      </div>
      <div class="deliveryTime">
        <span class="tip">送达时间</span>
        <span class="time">{{seller.deliveryTime}}分钟</span>
      </div>
    </div>
  </div>
  <filterRating :ratingFlag="'seller'" :tags="tags" :current="current" :ratings="ratings"></filterRating>
</div>
</template>

<script>
import axios from 'axios'
import star from './star'
import filterRating from './filterRating'
export default {
  data () {
    return {
      ratings:[],
      tags: {'全部':-1,'满意':1,'不满意':0},
      current: {type:'全部',text:false}
    }
  },
  props:{
    seller:{
      type:Object
    }
  },
  created(){
    axios.get('/good/ratings').then(
      res => {
        if(res.data.code === 0) {
          this.ratings = res.data.data;
          console.log(this.ratings)
        }
      }
    );
  },
  components:{
    star,
    filterRating
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus">
@import '../../static/style.css';
.seller-ratings
  background #f3f5f7
  .general-rating
    display flex
    border-bottom 1px solid rgba(7,17,27,.1)
    background #fff
    .left
      margin 15px 0
      padding 0 10px
      border-right 1px solid rgba(7,17,27,.1)
      text-align center
      .score
        font-size 24px
        color rgb(255,153,0)
      .tip
        margin 6px 0 8px
        font-size 12px
        color rgb(7,17,27)
      .rankRate
        font-size 10px
        color rgb(147,153,159)
    .right
      flex 1
      padding 15px 10px
      font-size 12px
    .star-rating
      margin-bottom 8px
      .stars
        display inline-block
        margin 0 2px
        vertical-align middle
      .tip
        color rgb(7,17,27)
        vertical-align middle
      .score
        color rgb(255,153,0)
        vertical-align middle
    .deliveryTime
      .tip
        margin-right 2px
        font-size 12px
        color rgb(7,17,27)
      .time
        color rgb(147,153,159)
</style>
