<template>
	<div>
		<div class="search">
			<input v-model="keyword" type="text" placeholder="输入城市名或拼音" class="search-input">
		</div>
		<div class="search-content" ref="search" v-show="keyword">
			<ul>
				<li class="search-item border-bottom" v-for="item of list" :key="item.id" @click="handleCityClick(item.name)">{{item.name}}</li>
				<li class="search-item border-bottom" v-show="hasNoList">没有找到匹配数据</li>
			</ul>
		</div>
	</div>
</template>

<script>
	import {mapMutations} from 'vuex'
	import Bscroll from 'better-scroll'
	export default{
		name:"CitySearch",
		props:{
			cities:Object
		},
		data(){
			return{
				keyword:'',
				list:[],
				timer:null
			}
		},
		computed:{
			hasNoList(){
				return !this.list.length
			}
		},
		watch:{
			keyword(){
				if(this.timer){
					clearTimeout(this.timer)
				}
				if(!this.keyword){
					this.list = []
					return
				}
				this.timer = setTimeout(()=>{
					const result = [];
					for(let i in this.cities){
						this.cities[i].forEach((value) => {
							if(value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1){
								result.push(value)
							}
						})
					}
					this.list = result
				},5)
			}
		},
		methods:{
			handleCityClick(city){
				//this.$store.commit("changeCity",city)
				this.changeCity(city)
				this.$router.push('/')
				//console.log(city)
			},
			...mapMutations(['changeCity'])
		},
		mounted () {
			this.scroll = new Bscroll(this.$refs.search)
		}
	}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.search{
		height:0.72rem;
		padding:0.1rem;
		background:$bgColor;
		.search-input{
			height:0.62rem;
			line-height:0.62rem;
			text-align:center;
			width:100%;
			border-radius:0.06rem;
			color:#666;
			box-sizing:border-box;
			padding:0 0.2rem;
		}
	}
	.search-content{
		overflow:hidden;
		z-index :1;
		position:absolute;
		top:1.58rem;
		left:0;
		right:0;
		bottom:0;
		background:#eee;
		.search-item{
			line-height:0.62rem;
			padding-left:0.2rem;
			color:#666;
			background:#fff;
		}
	}
</style>