<template>
	<view class="index-list animate__animated animate__fadeInLeft animate__fast">
		<view class="index-list1 u-f u-f-ac u-f-jsb">
			<view class="u-f u-f-ajc">
				<image :src="item.userpic" 
				mode="widthFix" 
				lazy-load></image>
				{{item.username}}
			</view>
			<view class="u-f u-f-ajc" v-if="item.isguanzhu" @tap="guanzhu">
				<view class="icon iconfont icon-jia"></view>
				关注
			</view>
			<view class="u-f u-f-ajc" v-else @tap="quguan">
				<view class="icon iconfont icon-quxiao"></view>
				取关
			</view>
		</view>
		<view class="index-list2" @tap="openDetail">{{item.title}}</view>
		<view class="index-list3 u-f u-f-ajc"  @tap="openDetail">
			<!-- 图片 -->
			<image :src="item.titlepic" 
			mode="widthFix" 
			lazy-load></image>
			<!-- 视频 -->
			<template v-if="item.type==='video'">
				<view class="index-list-play icon iconfont icon-bofang"></view>
				<view class="index-list-playinfo">
					{{item.playnum}}次播放 {{item.long}}
				</view>
			</template>
		</view>
		<view class="index-list4 u-f u-f-ac u-f-jsb">
			<view class="u-f u-f-ac">
				<view class="u-f u-f-ac">
					<view 
					class="icon iconfont icon-xiaolian" 
					:class="[item.infonum.index===1?'ding':'']"
					@tap="caozuo('ding')"></view>
					{{item.infonum.dingnum}}
					</view>
				<view class="u-f u-f-ac">
					<view 
					class="icon iconfont icon-kulian" 
					:class="[item.infonum.index===2?'cai':'']"
					@tap="caozuo('cai')"></view>
					{{item.infonum.cainum}}
					</view>
			</view>
			
			<view class="u-f u-f-ac">
				<view class="u-f u-f-ac">
					<view class="icon iconfont icon-liuyan"></view>
					{{item.commentnum}}
					</view>
				<view class="u-f u-f-ac">
					<view class="icon iconfont icon-fenxiang"></view>
					{{item.sharenum}}
					</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods:{
			/* 关注 */
			guanzhu(){
				this.item.isguanzhu=!this.item.isguanzhu
				uni.showToast({
					title: "关注成功"
				})
			},
			/* 取关 */
			quguan(){
				this.item.isguanzhu=!this.item.isguanzhu
				uni.showToast({
					title: "取关成功"
				})
			},
			/* 顶踩 */
			caozuo(type){
				switch(type){
					case "ding":
						if(this.item.infonum.index === 1)
						{
							return;
						}
						this.item.infonum.dingnum++
						if(this.item.infonum.index === 2)
						{
							this.item.infonum.cainum--
						}
						this.item.infonum.index = 1
						break;
					case "cai":
						if(this.item.infonum.index === 2)
						{
							return;
						}	
						this.item.infonum.cainum++
						if(this.item.infonum.index === 1)
						{
							this.item.infonum.dongnum--
						}
						this.item.infonum.index = 2
						break;
				}
			},
			openDetail(){
				uni.navigateTo({
					url: "../../pages/detail/detail?detailData="+JSON.stringify(this.item)	
				})
			}
		}
	}
</script>

<style lang="less" scoped>
.index-list{
		padding: 20upx;
		border-bottom: 1upx solid #EEEEEE;
		
		&>view{
			color: #999999;
		}
	}
	
	.index-list1>view:last-child{
		background-color: #F4F4F4;
		border-radius: 5upx;
		color: #000000;
		padding: 0 10upx;
	}
	.index-list1>view:first-child image{
		width: 90upx;
		height: 90upx;
		border-radius: 100%;
		margin-right: 10upx;
	}
	.index-list2{
		padding-top: 15upx;
		font-size: 32upx;
	}
	.index-list3{
		padding-top: 15upx;
		position: relative;
		
		&>.index-list-play {
			position: absolute;
			font-size: 120upx;
			color: #FFFDEF;
		}
		
		&>.index-list-playinfo{
			position: absolute;
			background-color: rgba(51, 51, 51, 0.7);
			color: #FFFFFF;
			bottom: 8upx;
			right: 8upx;
			border-radius: 40upx;
			font-size: 22upx;
			padding: 0 12upx;
		}
		
		&>image{
			width: 100%;
			border-radius: 20upx;
		}
	}
	
	.index-list4{
		padding: 15upx 0;
		color: #999999;
		
		&>view{
			&>view{
				margin-right: 15upx;
			}
		}
	}
	.ding{
		color: yellow;
	}
	.cai{
		color: red;
	}
</style>
