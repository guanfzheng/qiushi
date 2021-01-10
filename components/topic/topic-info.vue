<template>
	<view>
		<!-- 模糊背景 -->
		<view class="topic-bg">
			<image 
			:src="topicInfo.titlepic" 
			mode="aspectFill"
			lazy-load></image>
		</view>
		<!-- 话题信息 -->
		<view class="topic-info">
			<view class="topic-head u-f u-f-ac">
				<image 
				:src="topicInfo.titlepic" 
				mode="aspectFit"
				lazy-load></image>
				<view class="topic-title">{{topicInfo.title}}</view>
			</view>
			
			<view class="topic-dynamic u-f u-f-ac">
				<view>动态 {{topicInfo.totalnum}}</view>
				<view>今日 {{topicInfo.todaynum}}</view>
			</view>
			<view class="topic-desc">{{topicInfo.desc}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		},
		props: {
			topicInfo: Object
		}
	}
</script>

<style lang="less" scoped>
	.topic-bg{
		width: 100%;
		height: 300upx;
		position: relative;
		overflow: hidden;
		
		image{
			width: 100%;
			position: absolute;
			filter: blur(10px);
		}
	}
	
	.topic-info {
		padding: 0 25upx;
		
		.topic-head{
			position: relative;
			
			&>image{
				width: 150upx;
				height: 150upx;
				border-radius: 20upx;
				position: absolute;
				top: -75upx;
			}
			&>view{
				font-size: 30upx;
				margin-left: 180upx;
				flex: 1;
			}
		}
		.topic-dynamic{
			padding: 30upx 0 20upx 0;
			view {
				color: #CDCDCD;
				
			}
		}
		.topic-desc{
			color: #A3A3A3;
			font-size: 32upx;
			padding: 10upx 0 10upx 0;
		}
	}
</style>
