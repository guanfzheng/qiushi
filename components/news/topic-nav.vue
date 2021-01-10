<template>
	<!-- 热门分类 -->
	<view class="top-nav">
		<view class="u-f u-f-ac u-f-jsb">
			<view>热门分类</view>
			<view class="u-f u-f-ac" @tap="openTopicNav">更多<view class="icon iconfont icon-jinru"></view></view>
		</view>
		<view class="u-f u-f-ajc">
			<block v-for="(item, index) in nav">
				<view class="u-f u-f-ajc">{{item.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			nav: Array
		},
		methods: {
			openTopicNav(){
				uni.navigateTo({
					url:"../../pages/topic-nav/topic-nav"
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.top-nav{
		border-bottom: 1upx solid #EEEEEE;
		border-top: 1upx solid #EEEEEE;
		padding: 20upx;
		
		&>view:first-child{
			margin-bottom: 10upx;
			view{
				color:#9E9E9E;
			}
			&>view:first-child{
					color: #333333;
					font-size: 32upx;
				}
			
		}
		
		&>view:last-child{
			&>view{
				flex: 1;
				background-color: #dddddd;
				color: #9E9E9E;
				border-radius: 10upx;
				margin: 0 10upx;
			}
		}
	}
</style>
