<template>
	<div class="cartcontrol">
		<div class="cart-desc icon-remove_circle_outline" v-show="food.count>0" @click="descCart"></div>
		<div class="count" v-show="food.count>0">{{food.count}}</div>
		<div class="cart-add icon-add_circle" @click="addCart"></div>
	</div>
</template>

<!--suppress JSUnresolvedFunction, JSUnresolvedVariable -->
<script type="text/ecmascript-6">
	import Vue from 'vue'
	export default {
		props: {
			food: {
				type: Object
			}
		},
		methods: {
			addCart (event) {
				if (!event._constructed) {
					return;
				}
				if (!this.food.count) {
					Vue.set(this.food, 'count', 1);
				} else {
					this.food.count++;
				}
			},
			descCart (event) {
				if (!event._constructed) {
					return;
				}
				if (this.food.count) {
					this.food.count--;
				}
			}
		}
	}

</script>

<style lang="stylus" rel="stylesheet/stylus">
	.cartcontrol
		font-size: 0
		.cart-desc, .cart-add
			display: inline-block
			padding: 6px
			font-size: 24px
			line-height: 24px
			color: rgb(0, 160, 220)
		.count
			display: inline-block
			vertical-align: top
			padding-top: 6px
			width: 12px
			text-align: center
			font-size: 10px
			line-height: 24px
			color: rgb(147, 153, 159)

</style>
