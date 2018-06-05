<template>
  <div class="star-wrapper">
    <span class="icon on" :class="itemClass" v-for="item in starOn" :key="'on'+item"></span>
    <span class="icon half" :class="itemClass" v-show="starHalf != 0" ></span>
    <span class="icon off" :class="itemClass" v-for="item in starOff" :key="'off'+item" ></span>
  </div>
</template>

<script>
export default{
  props:{
    score:{
      type: Number,
      default: 0
    },
    itemClass:{
      type: String,
      default: 'star24'
    }
  },
  computed:{
    half(){
      return this.score * 10 % 10;
    },
    starOn(){
      if(this.half > 7){
        return Math.ceil(this.score);
      }else{
        return Math.floor(this.score);
      }
    },
    starHalf(){
      if(this.half >= 3 && this.half <= 7){
        return 1;
      }else{
        return 0;
      }
    },
    starOff(){
      return 5 - this.starOn - this.starHalf
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../assets/stylus/index.styl'
.star-wrapper
  text-align center
  .icon
    display inline-block
  .star48
    width: 20px;
    height: 20px;
    &:nth-child(n+2)
      margin-left: 22px;
    background-size: 20px 20px;
    &.on
      bg-image('star48_on')
    &.half
      bg-image('star48_half')
    &.off
      bg-image('star48_off')
  .star36
    width: 15px;
    height: 15px;
    &:nth-child(n+2)
      margin-left: 3px;
    background-size: 15px 15px;
    &.on
      bg-image('star36_on')
    &.half
      bg-image('star36_half')
    &.off
      bg-image('star36_off')
  .star24
    width: 10px;
    height: 10px;
    &:nth-child(n+2)
      margin-left: 3px;
    background-size: 10px 10px;
    &.on
      bg-image('star24_on')
    &.half
      bg-image('star24_half')
    &.off
      bg-image('star24_off')
</style>
