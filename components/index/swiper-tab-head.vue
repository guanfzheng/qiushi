<template>
	<!-- 顶部选项卡 -->
	<view class="uni-tab-bar">
		<scroll-view scroll-x class="uni-swiper-tab" :style="scrollStyle">
			<block v-for="(tab, index) in tabBars" :key="tab.id">
				<view 
				class="swiper-tab-list" 
				:class="{'active':tabIndex===index}"
				@tap="taptab(index)"
				:style="scrollItemStyle">
					{{tab.name}} {{tab.num?tab.num:''}}
					<view class="swiper-tab-line"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		methods:{
			taptab(index){
				this.$emit("tabtap",index)
			}
		},
		props:{
			tabBars: Array,
			tabIndex: Number,
			scrollItemStyle: {
				type: String,
				default: ""
			},
			scrollStyle: {
				type: String,
				default: ""
			}
		}
	}
</script>

<style lang="less" scoped>
	.swiper-tab-list{
		color: #969696;
		font-weight: bold;
	}
	.uni-tab-bar {
		.uni-swiper-tab{
			border-bottom: 1upx solid #EEEEEE;
		}
		
		.active{
			color: #343434;
			
			.swiper-tab-line{
				border-bottom: 6upx solid #EFDE33;
				width: 60%;
				margin: auto;
			}
		}
	}
	
</style>

