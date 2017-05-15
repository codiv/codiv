<template>
	<div class="shopcart">
		<div class="content">
			<div class="content-left">
				<div class="logo-wrapper">
					<div class="logo" :class="{'highLight':totalCount>0}"><i class="icon-shopping_cart"></i></div>
					<div class="num" v-show="totalCount>0">{{totalCount}}</div>
				</div>
				<div class="price" :class="{'highLight':totalPrice>0}">￥{{totalPrice}}</div>
				<div class="desc">
					另需配送费￥{{deliveryPrice}}元
				</div>
			</div>
			<div class="content-right">
				<div class="pay" :class="payClass">{{payDecs}}</div>
			</div>
		</div>
	</div>
</template>

<!--suppress JSUnresolvedVariable -->
<script type="text/ecmascript-6">
	export default {
		props: {
			selectFoods: {
				type: Array,
				default () {
					return [
						{
							price: 10,
							count: 1
						}
					]
				}
			},
			minPrice: {
				type: Number,
				default: 0
			},
			deliveryPrice: {
				type: Number,
				default: 0
			}
		},
		computed: {
			totalPrice () {
				let total = 0;
				this.selectFoods.forEach(function (food) {
					total += food.price * food.count;
				});
				//简写
//				this.selectFoods.forEach((food) => {
//					total += food.price * food.count;
//				});
				return total;
			},
			totalCount () {
				let count = 0;
				this.selectFoods.forEach((food) => {
					count += food.count;
				});
				return count;
			},
			payDecs () {
				if (this.totalPrice === 0) {
					return `￥${this.minPrice}元起送`
				} else if (this.totalPrice < this.minPrice) {
					let def = this.minPrice - this.totalPrice
					return `还差￥${def}元起送`
				} else {
					return '去结算！'
				}
			},
			payClass () {
				if (this.totalPrice < this.minPrice) {
					return 'not-enough'
				} else {
					return 'enough'
				}
			}
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"
	.shopcart
		position: fixed
		left: 0
		bottom: 0
		z-index: 50
		height: 48px
		width: 100%
		.content
			display: flex
			background-color: #141d27
			font-size: 0
			height: 48px
			color: rgba(255, 255, 255, 0.4)
			.content-left
				flex: 1
				.logo-wrapper
					display: inline-block
					position: relative
					top: -10px
					border-radius: 50%
					margin: 0 12px
					padding: 6px
					width: 56px
					height: 56px
					box-sizing: border-box
					background-color: #141d27
					.logo
						width: 100%
						height: 100%
						border-radius: 50%
						text-align: center
						background-color: #2b343c
						.icon-shopping_cart
							line-height: 44px
							font-size: 24px
							color: #80858a
						&.highLight
							background-color: #00a0dc
							.icon-shopping_cart
								color: #FFF
					.num
						position: absolute
						top: 0
						right: 0
						width: 24px
						height: 16px
						line-height: 16px
						text-align: center
						border-radius: 16px
						font-size: 9px
						font-weight: 700
						color: #fff
						background: #f01414
						box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)
				.price
					display: inline-block
					vertical-align: top
					margin-top: 12px
					line-height: 24px
					padding-right: 12px;
					box-sizing: border-box
					border-right: 1px solid rgba(255, 255, 255, 0.1)
					font-size: 16px
					font-weight: 700
					&.highLight
						color: #FFF
				.desc
					display: inline-block
					vertical-align: top
					margin: 12px 0 0 12px
					line-height: 24px
					font-size: 10px
			.content-right
				flex: 0 0 105px
				width: 105px
				.pay
					height: 48px
					line-height: 48px
					text-align: center
					font-size: 12px
					font-weight: 700
					&.not-enough
						background-color: #2b333b
					&.enough
						background-color: #00b43c
						color: #FFF


</style>
