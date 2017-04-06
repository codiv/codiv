<template>
	<div id="goods">
		<div class="menu-wrapper" ref="menuWrapper">
			<ul>
				<li v-for="item in goods" class="menu-item">
					<span class="text border-1px">
						<em class="icon" v-if="item.type>0" :class="classMain[item.type]"></em>{{item.name}}
					</span>
				</li>
			</ul>
		</div>
		<div class="food-wrapper"></div>

	</div>

</template>

<script type="text/ecmascript-6">
	let ERR_OK = 0
	export default{
		data () {
			return {
				goods: {
					type: Object
				},
				classMain: {
					type: Array
				}
			}
		},
		created () {
			this.$http.get('api/goods', {name: "abc"}).then((response) => {
				let res = response.body
				if (res.errno === ERR_OK) {
					this.goods = res.data
					this.$nextTick(() => {
						wrapperScroll ()
					})
				}
			}),
			this.classMain = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
		},
		methods: {
			wrapperScroll () {
				let menuWrapper = new BScroll(this.$refs.menuWarpper,{
					probeType: 3
				})
				menuWrapper.on('scroll', (pos) => {
					console.log(pos.x + '~' + posx.y)
				})
			}
		}
	}

</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl"
	#goods
		display: flex
		position: absolute
		top: 174px
		bottom: 46px
		width: 100%
		overflow: hidden
		.menu-wrapper
			flex: 0 0 80px
			width: 80px
			background: #f3f5f7
			.menu-item
				display: table
				height: 54px
				width: 56px
				padding: 0 12px
				line-height: 14px
				font-size: 0
				.text
					display: table-cell
					width: 56px
					vertical-align: middle
					font-size: 12px
					border-1px(rgba(7, 17, 27, 0.2))
					.icon
						display: inline-block
						width: 12px
						height: 12px
						margin-right: 2px
						background-size: 12px 12px
						background-repeat: no-repeat
						vertical-align: top
						&.decrease
							bg-images("decrease_3")
						&.discount
							bg-images("discount_3")
						&.guarantee
							bg-images("guarantee_3")
						&.invoice
							bg-images("invoice_3")
						&.special
							bg-images("special_3")
		.food-wrapper
			flex: 1


</style>
