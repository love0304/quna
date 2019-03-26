<template>
	<div class="wrapper">
		<swiper :options="swiperOption" v-if="list.length">
		    <!-- slides -->
		    <swiper-slide v-for="item of list" :key="item.id">
		    	<img class="swiper-img" :src="item.imgUrl" alt="">
		    </swiper-slide>
		    <div class="swiper-pagination"  slot="pagination"></div>
		</swiper>
	</div>
</template>

<script>
export default {
	name:"HomeSwiper",
	props:{
		list: Array
	},
	data:function(){
		return{
			swiperOption:{
				pagination:'.swiper-pagination',
				loop:true,//图片无限转动
				autoplay:3000,
				autoplayDisableOnInteraction : false //解决用户点击之后不自动轮播问题
			}
		}
	}
}
</script>

<style lang="stylus" scoped>
	.wrapper >>> .swiper-pagination-bullet-active{
			background:#fff;
		}
	.wrapper{
		width:100%;
		height:0;
		overflow:hidden;
		padding-bottom:26.75%;
		background:#eee;

		.swiper-img{
			width:100%
		}
	}
	
</style>