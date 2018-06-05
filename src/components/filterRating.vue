<template>
<div class="filter-container">
  <div class="item-wrapper">
    <div class="title" v-show="ratingFlag === 'food'">商品评价</div>
    <ul class="filter-wrapper">
      <li class="item" v-for="(item,index) in tags" :key="index" :class="{'active':current.type === index}" @click="changeCurrent(index)">
        {{index}}<span>{{filterRating.ratingLen[index]}}</span>
      </li>
    </ul>
    <div class="filter" :class="{'active':current.text}" @click="changeText()">
      <span class="icon-check_circle"></span>
      <span class="text">只看有内容的评价</span>
    </div>
  </div>
  <sellerRating :filterRating="filterRating.ratings" :timestampToTime="timestampToTime" v-show="ratingFlag === 'seller'"></sellerRating>
  <foodRating :filterRating="filterRating.ratings" :timestampToTime="timestampToTime" v-show="ratingFlag === 'food'"></foodRating>
</div>
</template>

<script>
import sellerRating from './sellerRating'
import foodRating from './foodRating'
export default {
  data () {
    return {
      msg:''
    }
  },
  props:{
    ratingFlag:{
      type:String
    },
    tags:{
      type:Object
    },
    current:{
      type:Object
    },
    ratings:{
      type:Array
    }
  },
  computed:{
    filterRating(){
      let ratings = this.ratings;
      let ratingLen = {'全部':0,'推荐':0,'吐槽':0}
      if(this.current.text){
        ratings = ratings.filter(rating => rating.text !== '');
        ratingLen['全部'] = ratings.length;
      }else{
        ratingLen['全部'] = ratings.length;
      }
      if(this.current.type !== '全部'){
        ratings = ratings.filter(rating => rating.rateType === this.tags[this.current.type]);
        if(this.current.type == '推荐'){
          ratingLen['推荐'] = ratings.length;
          ratingLen['吐槽'] = ratingLen['全部'] - ratingLen['推荐'];
        }else{
          ratingLen['吐槽'] = ratings.length;
          ratingLen['推荐'] = ratingLen['全部'] - ratingLen['吐槽'];
        }
      }else{
        ratings.forEach((rating) => {
          if(rating.rateType === 1){
            ratingLen['推荐'] ++;
          }else{
            ratingLen['吐槽'] ++;
          }
        })
      }
      return {ratings,ratingLen};
    }
  },
  methods:{
    changeCurrent(tag){
      this.current.type = tag;
    },
    changeText(){
      this.current.text = !this.current.text;
    },
    timestampToTime(timestamp) {
      let date = new Date(timestamp);
      let Y = date.getFullYear() + '-',
          M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-',
          D = date.getDate() + ' ',
          h = date.getHours() + ':',
          m = date.getMinutes();
      return Y+M+D+h+m;
    }
  },
  components:{
    sellerRating,
    foodRating
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus">
@import '../../static/style.css';
.filter-container
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
  .filter-wrapper
    margin 0 18px
    padding 12px 0 18px
    border-bottom 1px solid rgba(7,17,27,.1)
    .item
      display inline-block
      padding 8px 12px
      border-radius 4px
      font-size 14px
      color rgb(77,85,93)
      background rgba(77,85,93,.2)
      &:nth-child(n+2)
        margin-left 8px
      span
        padding-left 4px
        font-size 12px
      &.active
        color #fff
        background rgb(0,160,220)
  .filter
    padding 12px 18px
    color rgb(147,153,159)
    &.active
      .icon-check_circle
        color rgb(0,160,220)
    .icon-check_circle
      display inline-block
      vertical-align middle
    .text
      font-size 12px
</style>
