<template>
	<view class="user-list u-f u-f-ac animate__animated animate__fadeInLeft animate__fast">
		<image :src="user.userpic" mode="widthFix" lazy-load></image>
		<view>
			<view>{{user.username}}</view>
			<tag-sex-age :sex="user.sex" :age="user.age"></tag-sex-age>
		</view>
		<view v-if="user.isguanzhu" class="icon iconfont icon-dagou u-f u-f-ajc"></view>
		<view v-else class="icon iconfont icon-jiahao u-f u-f-ajc"></view>
	</view>
</template>

<script>
	import tagSexAge from '../../components/common/tag-sex-age.vue';
	export default {
		props: {
			user: Object
		},
		components: {
			tagSexAge
		}
	}
</script>

<style lang="less" scoped>
	/* 好友列表 */
	.user-list{
		padding: 20upx 0;
		border-bottom: 1upx solid #EEEEEE;
		
		image{
			width: 100upx;
			height: 100upx;
			border-radius: 100%;
			margin-right: 20upx;
			flex-shrink: 0;
		}
		&>view:first-of-type{
			flex: 1;
			&>view:first-child{
				font-size: 35upx;
			}
		}
		
		&>view:last-of-type{
			width: 80upx;
			color: #CCCCCC;
			margin-right: 60upx;
		}
		
		.icon-jiahao{
			color: #F8791B !important;
		}
	}
</style>
