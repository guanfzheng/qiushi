<template>
	<view class="other-login u-f u-f-ac">
		<view class="u-f u-f-ajc u-f1"><view class="icon iconfont icon-logo-wechat u-f u-f-ajc"></view></view>
		<view class="u-f u-f-ajc u-f1"><view class="icon iconfont icon-weibo u-f u-f-ajc"></view></view>
		<view class="u-f u-f-ajc u-f1"><view class="icon iconfont icon-qq u-f u-f-ajc"></view></view>
	</view>
</template>

<script>
	export default {
		
	}
</script>

<style>
.other-login{
	padding: 20upx 80upx;
}
.other-login>view{
	flex: 1;
}
.other-login>view>view{
	width: 100upx;
	height: 100upx;
	border-radius: 100%;
	font-size: 55upx;
	color: #FFFFFF;
}
.other-login .icon-qq{
	background: #2CAEFC;
}
.other-login .icon-logo-wechat{
	background: #2BD19B;
}
.other-login .icon-weibo{
	background: #FC7729;
}
</style>
