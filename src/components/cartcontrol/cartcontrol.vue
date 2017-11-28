<template>
	<div class="cartcontrol">
		<div class="cart-decrease" v-show="food.count>0" @click="decreaseCart($event)" transiton="move">
			<span class="inner icon-remove_circle_outline"></span>
		</div>
		<div class="cart-count" v-show="food.count>0">{{food.count}}</div>
		<div class="cart-add icon-add_circle" @click="addCart($event)"></div>
	</div>
</template>

<script type="text/ecmascript-6">
	import Vue from 'vue';

	export default {
		props: {
			food: {
				type: Object
			}
		},
		methods: {
			addCart(event) {
				if (!event._constructed) {
					return;
				}
				if (!this.food.count) {
					// this.food.count = 1;
					/* 添加对象没有的属性时，需要用vue包装好的方法，否则检测不到 */
					Vue.set(this.food, 'count', 1);
				} else {
					this.food.count++;
				}
				this.$dispatch('cart.add', event.target);
			},
			decreaseCart(event) {
				if (!event._constructed) {
					return;
				}
				if (this.food.count) {
					this.food.count--;
				}
			}
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	.cartcontrol
		font-size: 0
		.cart-decrease
			display: inline-block
			padding: 6px
			line-height: 24px
			font-size: 24px
			color: rgb(0, 160, 220)
			&.move-transition
				opacity: 1
				transform: translate3d(0, 0, 0)
				transition: all 0.4s linear
				.inner 
					display: inline-block
					transition: all 0.4s linear
					transform: rotate(0)
			&.move-enter, &.move-leave
				opacity: 0
				transform: translate3d(24px, 0, 0)
				.inner
					transform: rotate(180deg)
		.cart-count   
			display: inline-block 
			width: 12px
			padding-top: 6px
			vertical-align: top
			line-height: 24px
			font-size: 14px
			color: rgb(147, 153, 159)
		.cart-add
			display: inline-block
			padding: 6px
			line-height: 24px
			font-size: 24px
			color: rgb(0, 160, 220)
</style>