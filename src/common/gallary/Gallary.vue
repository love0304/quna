<template>
	<div class="container" @click="handleGallaryClick">
		<div class="wrapper">
			<swiper :options="swiperOptions">
			    <swiper-slide v-for="(item,index) in imgs" :key="index">
			    	<img class="gallary-img" :src="item" alt="">
			    </swiper-slide>
			    <div class="swiper-pagination"  slot="pagination"></div>
			</swiper>
		</div>
	</div>
</template>

<script>
	export default {
		name:'CommonGallary',
		props:{
			imgs:{
				type:Array,
				default(){
					return []
				}
			}
		},
		methods:{
			handleGallaryClick(){
				this.$emit('close')
			}
		},
		data(){
			return{
				swiperOptions:{
					pagination:".swiper-pagination",
					paginationType:'fraction',
					observeParents:true,
					observer:true
				}
			}
		}
	}
</script>

<style lang="stylus" scoped>
	.container >>> .swiper-container{
		overflow:inherit;
	}
	.container{
		position:fixed;
		left :0px;
		right :0px;
		top:0px;
		bottom:0px;
		background:#000;
		z-index :99;
		display :flex;
		flex-direction :column;
		justify-content :center;
		.wrapper{
			width:100%;
			height:0;
			padding-bottom:100%;
			.gallary-img{
				width:100%;
			}
			.swiper-pagination{
				color:#fff;
				bottom:-1rem;
			}
		}
	}
</style>