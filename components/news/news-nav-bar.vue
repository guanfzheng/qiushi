<template>
	<view>
		<!-- 自定义导航 -->
		<uni-nav-bar
		:statusBar="true" 
		@clickLeft="signIn" 
		@clickRight="summit"
		:fixed="true"
		:border="false">
			<block slot="left" ><view class="icon iconfont icon-qiandao"></view></block>
			<view class="nav-center u-f u-f-ajc">
				
				<block v-for="(item, index) in tabBars" :key="item.id">
					<view class="u-f u-f-ajc" 
					:class="{'active': tabIndex === index}"
					@tap="changeTab(index)">
					{{item.name}}
					<view v-if="tabIndex === index" class="nav-center-line"></view>
				</view>
				</block>
			</view>
			<block slot="right"><view class="icon iconfont icon-bi"></view></block>
		</uni-nav-bar>
	</view>
</template>

<script>	
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue";
	
	export default {
		props: {
			tabBars: Array,
			tabIndex: Number
		},
		methods: {
			signIn(){
				console.log("signIn")
			},
			summit(){
				uni.navigateTo({
					url: "../add-input/add-input"
				})
			},
			changeTab(index){
				this.$emit("changeTab", index)
			},
		},
		components: {
			uniNavBar,
		}
	}
</script>

<style lang="less" scoped>
	.icon-qiandao{
		color: rgb(255, 150, 25);
		font-size: 40upx;
		text-align: center;
		flex: 1;
	}
	.icon-bi{
		color: #000000;
		font-size: 40upx;
		text-align: center;
	}
	.nav-center{
		flex: 1;
		position: relative;
		
		view{
			w
			font-size: 32upx;
			font-weight: bold;
			color: #969696;
			padding: 0 15upx;
		}
		.active{
			color: #333333 !important;
			
			.nav-center-line{
				border-bottom: 10upx solid #FEDE33;
				width: 50upx;
				border-radius: 20upx;
				position: absolute;
				bottom: -5upx;
				z-index: 99;
			}
		}
		
	}
	
</style>
