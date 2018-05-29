<template>
  <div class="control-wrapper">
    <span class="decrease icon-remove_circle_outline" v-show="food.count > 0" @click="remove"></span>
    <span class="count" v-show="food.count > 0">{{food.count}}</span>
    <span class="increase icon-add_circle add-icon" @click="add"></span>
  </div>
</template>

<script>
import Vue from 'vue';
export default{
  props:{
    food:{
      type:Object
    }
  },
  methods:{
    remove(event){
      // if(event._constructed){
        if(this.food.count === 0){
          return;
        }else{
          this.food.count --;
        }
      // }
    },
    // 绑定了一个bsscroll插件
    add(event){
      // if(event._constructed){
        if(!this.food.count){
          Vue.set(this.food, "count");
          this.food.count = 1;
        }else{
          this.food.count ++;
        }
      // }
    }
  }
}
</script>

<style lang="stylus" scoped>
.control-wrapper
  display flex
  color rgb(0,160,220)
  font-size 24px
  span
    flex 1
    display inline-block
    vertical-align middle
  .count
    font-size 10px
    color rgb(147,153,159)
</style>
