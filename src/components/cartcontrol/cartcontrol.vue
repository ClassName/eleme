<template>
  <div class="cartcontrol">
    <div @click.stop.prevent="decreaseCart" class="cart-decrease icon-remove_circle_outline" v-show="food.count > 0"></div>
    <div class="cart-count" v-show="food.count > 0">{{ food.count }}</div>
    <div @click.stop.prevent="addCart" class="cart-add icon-add_circle"></div>
  </div>
</template>

<script>
  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      addCart (event) {
        if (!event._constructed) {
          return
        }
        if (!this.food.count) {
          this.$set(this.food, 'count', 1)
        } else {
          this.food.count ++
        }
      },
      decreaseCart (event) {
        if (!event._constructed) {
          return
        }
        if (this.food.count) {
          this.food.count --
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
.cartcontrol
  font-size 0
  .cart-decrease,.cart-add
    font-size 24px
    line-height 24px
    display inline-block
    padding 6px
    color rgb(0,160,220)
  .cart-count
    display inline-block
    vertical-align top
    text-align center
    font-size 10px
    padding-top 6px
    line-height 24px
    color rgb(147, 153, 159)
</style>
