<template>
	<div class="header">
		城市选择
		<router-link to="/">
		<div class="iconfont header-back">&#xe624</div>
		</router-link>
	</div>
</template>

<script>
	export default{
		name:'CityHeader'
	}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.header{
		height:$headerHeight;
		line-height:$headerHeight;
		text-align:center;
		color:#fff;
		background:$bgColor;
		foun-size:0.32rem;
		position:relative;
		.header-back{
			width:0.64rem;
			top:0;
			left:0;
			font-size:0.4rem;
			text-align:center;
			position: absolute;
			color:#fff;
		}
	}
</style>