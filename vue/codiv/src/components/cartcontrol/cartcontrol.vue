<template>
	<div class="cartcontrol">
		<div class="cart-desc icon-remove_circle_outline"></div>
		<div class="count">11</div>
		<div class="cart-add icon-add_circle"></div>
	</div>
</template>

<script type="text/ecmascript-6">
	export default {}

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
