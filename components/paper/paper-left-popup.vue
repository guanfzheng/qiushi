<template>
	<view>
		<!-- 操作列表 -->
		<view class="paper-left-popup-mask" v-show="show" @tap="hidepopup"></view>
		<view class="paper-left-popup" v-show="show">
			<view class="u-f u-f-ac" hover-class="paper-left-popup-h" @tap="addfriend">
				<view class="icon iconfont icon-sousuo">加糗友</view>
			</view>
			<view class="u-f u-f-ac" hover-class="paper-left-popup-h" @tap="clear">
				<view class="icon iconfont icon-qingchu">清除缓存</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				
			}
		},
		methods: {
			hidepopup(){
				this.$emit("hide")
			},
			addfriend(){
				this.$emit("addfirend")
			},
			clear(){
				this.$emit("clear")
			}
		},
		props: {
			show: Boolean
		}
	}
</script>

<style lang="less" scoped>
	.paper-left-popup-mask{
		position: fixed;
		right: 0;
		top: 0;
		bottom: 0;
		left: 0;
		z-index: 1999;
	}
	.paper-left-popup{
		position: fixed;
		right: 0;
		top: 80upx;
		background: #FFFFFF;
		z-index: 2000;
		width: 55%;
		box-shadow: 1upx 1upx 20upx 20upx #CCCCCC;
		&>view{
			padding: 20upx;
			font-size: 35upx;
			&>view{
				margin-right: 10upx;
			}
		}
		
		.paper-left-popup-h{
			background: #EEEEEE;
		}
	}
</style>
