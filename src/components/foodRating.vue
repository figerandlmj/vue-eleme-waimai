<template>
<ul class="foodRatings-wrapper">
  <li v-for="rating in filterRating" :key="rating.id">
    <div class="left">
      <div class="time">{{timestampToTime(rating.rateTime)}}</div>
      <div class="text-wrapper">
        <span :class="[{'icon-thumb_down': rating.rateType===0}, {'icon-thumb_up': rating.rateType===1}]"></span>
        <span class="text">{{rating.text}}</span>
      </div>
    </div>
    <div class="right">
      <span>{{rating.username}}</span>
      <img :src="rating.avatar">
    </div>
  </li>
</ul>
</template>

<script>
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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" ref="stylesheet/stylus">
@import '../../static/style.css';
.foodRatings-wrapper
  margin-bottom 48px
  background #fff
  li
    display flex
    margin 0 18px
    padding 16px 0
    font-size 10px
    color rgb(147,153,159)
    &:nth-child(n+2)
      border-top 1px solid rgba(7,17,27,.1)
  .left
    flex 1
    .time
      margin-bottom 6px
    .text-wrapper
      span
        display inline-block
        vertical-align middle
      .icon-thumb_up
         color rgb(0,160,220)
      .text
        font-size 12px
        color rgb(7,17,27)
  .right
    img
      width 12px
      height 12px
      border-radius 50%
</style>
