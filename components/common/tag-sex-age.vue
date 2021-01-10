<template>
	<view class="tag-sex">
		<view class="icon iconfont icon-nan" v-if="sex===0">{{age}}</view>
		<view class="icon iconfont icon-nv" v-else>{{age}}</view>
	</view>
</template>

<script>
	export default {
		props: {
			sex: Number,
			age: Number
		}
	}
</script>

<style lang="less" scoped>
	.tag-sex{
		width: 90upx;
		view{
			font-size: 12upx;
			background-color: #007AFF;
			color: #FFFFFF;
			padding: 0 10upx;
			margin-left: 12upx;
			border-radius: 20upx;
			line-height: 30upx;
		}
		.icon-nv{
			background-color: #FF498D !important;
		}
	}
</style>
