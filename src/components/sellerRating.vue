<template>
<ul class="sellerRatings-wrapper">
  <li v-for="rating in filterRating" :key="rating.id">
    <div class="left">
      <img :src="rating.avatar">
    </div>
    <div class="right">
      <div class="clearfix name-time">
        <span class="name">{{rating.username}}</span>
        <span class="time">{{timestampToTime(rating.rateTime)}}</span>
      </div>
      <div class="star-minute">
        <star :score="rating.score" :itemClass="'star24'" class="stars"></star>
        <span class="minute">{{rating.deliveryTime}}分钟送达</span>
      </div>
      <div class="text">{{rating.text}}</div>
      <div class="recommend-wrapper">
        <span class="icon" :class="[{'icon-thumb_down': rating.rateType===0}, {'icon-thumb_up': rating.rateType===1}]"></span>
        <span v-for="(item,index) in rating.recommend" :key="index" class="recommend">{{item}}</span>
      </div>
    </div>
  </li>
</ul>
</template>

<script>
import star from './star'
export default {
  data () {
    return {
    }
  },
  props:{
    filterRating:{
      type:Array
    },
    timestampToTime:{
      type:Function
    }
  },
  components:{
    star
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus">
@import '../../static/style.css';
.sellerRatings-wrapper
  background #fff
  li
    display flex
    margin 0 18px
    padding 18px 0
    &:nth-child(n+2)
      border-top 1px solid rgba(7,17,27,.1)
  .left
    img
      width 28px
      height 28px
      margin-right 12px
      border-radius 50%
  .right
    flex 1
    .name-time
      display flex
      font-size 10px
      .name
        text-align left
        color rgb(7,17,27)
      .time
        flex 1
        text-align right
        color rgb(147,153,159)
    .star-minute
      margin 2px 0 6px
      .stars
        display inline-block
        margin-right 6px
      .minute
        font-size 10px
        color rgb(147,153,159)
    .text
      margin-bottom 4px
      line-height 18px
      font-size 12px
      color rgb(7,17,27)
    .recommend-wrapper
      .icon
        vertical-align middle
      .icon-thumb_down
        color: #93999f;
      .icon-thumb_up
        color rgb(0,160,220)
      .recommend
        display inline-block
        margin-right 8px
        margin-top 4px
        padding 2px 4px
        border 1px solid rgba(7,17,27,.1)
        border-radius 2px
        text-align center
        font-size 12px
        color rgb(0,160,220)
</style>
