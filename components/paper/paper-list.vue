<template>
	<!-- 小纸条列表 -->
	<view class="paper-list u-f u-f-ac animate__animated animate__fadeInLeft animate__fast"
	@tap="openChatDetail">
		<image :src="paper.userpic" mode="widthFix" lazy-load></image>
		<view>
			<view class="u-f u-f-jsb">{{paper.username}}<view>{{paper.time}}</view></view>
			<view class="u-f u-f-jsb">{{paper.data}}
				<template v-if="paper.noreadnum>0">
					<uni-badge :text="paper.noreadnum" type="error"></uni-badge>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from "../../components/uni-badge/uni-badge.vue"
	export default {
		data(){
			return {
				
			}
		},
		props: {
			paper: Object
		},
		components: {
			uniBadge,
		},
		methods:{
			openChatDetail(){
				uni.navigateTo({
					url: "../../pages/user-chat/user-chat"
				})
			}
		},
		
	}
</script>

<style lang="less" scoped>
	.paper-list{
		border-bottom: 1upx solid #EEEEEE;
		padding: 20upx 0;
		
		image{
			width: 100upx;
			height: 100upx;
			border-radius: 100%;
			margin-right: 20upx;
			flex-shrink: 0;
		}
		&>view{
			flex: 1;
			&>view:first-child{
				font-size: 35upx;
				&>view{
					color: #CBCBCB;
					
				}
			}
			&>view:last-child{
				color: #999999;
			}
		}
	}
</style>
