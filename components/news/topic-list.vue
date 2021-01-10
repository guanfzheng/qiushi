<template>
	<view class="topic-list u-f u-f-ac">
		<image 
		:src="list.titlepic" 
		mode="widthFix"
		lazy-load></image>
		<view @tap="openTopicDetail">
			<view>{{list.title}}</view>
			<view>{{list.desc}}</view>
			<view>动态 {{list.totalnum}} 今日 {{list.todaynum}}</view>
		</view>
	</view>
	
</template>

<script>
	export default {
		props: {
			list: Object
		},
		methods: {
			openTopicDetail(){
				uni.navigateTo({
					url:"../../pages/topic-detail/topic-detail"
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	
	.topic-list{
		padding-inline-end: 10upx 0;
		border-bottom: 1upx solid #EEEEEE;
		image{
			width: 150upx;
			height: 150upx;
			border-radius: 10upx;
			margin-right: 20upx;
			
		}
		&>view{
			color: #A4A4A4;
			&>view:first-child{
				color: #333333;
				font-size: 32upx;
			}
		}
		
	}
</style>
