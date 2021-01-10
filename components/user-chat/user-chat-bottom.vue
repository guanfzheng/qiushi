<template>
	<view>
		<!-- 输入框 -->
		<view class="user-chat-bottom u-f u-f-ac">
			<input v-model="text" type="text" placeholder="文明发言" />
			<view class="icon iconfont icon-dongtai u-f u-f-ajc" @tap="submit"></view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data(){
			return {
				text: ""
			}
		},
		methods: {
			submit(){
				if(this.text !== '') {
					this.$emit("submit", this.text)
					this.text = ''
				}
			}
		}
	}
</script>

<style lang="less" scoped>
	.user-chat-bottom{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		height: 120upx;
		padding: 0 20upx;
		background-color: #FFFFFF;
		border-top: 1upx solid #EEEEEE;
		
		&>input{
			flex: 1;
			margin-right: 20upx;
			border-radius: 10upx;
			padding: 10upx 20upx;
			background: #F7F7F7;
		}
		&>view{
			width: 80upx;
			font-size: 45upx;
		}
	}
</style>
