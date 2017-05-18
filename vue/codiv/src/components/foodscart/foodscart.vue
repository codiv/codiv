<template>
	<div class="shopcart-list" v-show="listShow">
		<div class="list-header">
			<h1 class="title">购物车</h1>
			<span class="empty">清空</span>
		</div>
		<div class="list-content" ref="listContent">
			<ul>
				<li class="food border-1px" v-for="food in selectFoods">
					<span class="name">{{food.name}}</span>
					<div class="price">￥{{food.price*food.count}}</div>
					<div class="cartcontrol-wrapper">
						<cartcontrol :food="food" @add="addFood"></cartcontrol>
					</div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script type="text/ecmascript-6">
	import BScroll from 'better-scroll'
	import cartcontrol from 'components/cartcontrol/cartcontrol'

	export default{
		props: {
			selectFoods: {
				type: Array,
				default () {
					return []
				}
			},
			fold: {
				type: Boolean,
				default () {
					return true
				}
			}
		},
		created () {
			this.$nextTick(() => {
				this._listContent();
			})
		},
		methods: {
			addFood(target) {
				this.$refs.onshopcart.drop(target)
			},
			_listContent () {
				this.listContent = new BScroll(this.$refs.listContent, {
					click: true
				})
			},
			listShow () {
				return this.fold;
			}
		},
		components: {
			cartcontrol
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl";
	.shopcart-list
		position: absolute
		top: 0
		left: 0
		z-index: -1
		width: 100%
		.list-header
			height: 40px
			line-height: 40px
			padding: 0 18px
			background: #f3f5f7
			border-1px(rgba(7, 17, 27, 0.1))
			.title
				float: left
				font-size: 14px
				color: #07111b
			.empty
				float: right
				font-size: 12px
				color: #00a0dc
		.list-content
			padding: 0 18px
			max-height: 217px
			overflow: hidden
			background: #fff
			.food
				position: relative
				padding: 12px 0
				box-sizing: border-box
				border-1px(rgba(7, 17, 27, 0.1))
				.name
					line-height: 24px
					font-size: 14px
					color: #07111b
				.price
					position: absolute
					right: 90px
					bottom: 12px
					line-height: 24px
					font-size: 14px
					font-weight: 700
					color: #f01414
				.cartcontrol-wrapper
					position: absolute
					right: 0
					bottom: 6px
</style>
