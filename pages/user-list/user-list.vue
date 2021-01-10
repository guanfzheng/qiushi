<template>
	<view class="body">
		<!-- tab切换 -->
		<swiper-tab-head
		:tabBars="tabBars" 
		:tabIndex="tabIndex"
		@tabtap="tabtap"
		scrollStyle="border-bottom:0;" 
		scrollItemStyle="width:33%;"></swiper-tab-head>
		
		<view class="uni-tab-bar">
			<swiper 
			class="swiper-box" 
			:style="{height:swiperHeight+'px'}"
			:current="tabIndex"
			@change="tabChange">
				<swiper-item 
				v-for="(news,newsindex) in newsList" 
				:key="newsindex">
					<scroll-view scroll-y class="list" 
				@scrolltolower="loadmore(newsindex)">
						<template v-if="news.list.length>0">
							<!-- 好友列表 -->
							<block v-for="(item, index) in news.list" :key="index">
								<user :user="item"></user>
							</block>
							<!-- 上拉加载 -->
							<load-more :loadtext="news.loadtext"></load-more>
						</template>
						<template v-else>
							<no-thing></no-thing>
						</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
		
	</view>
</template>

<script>
	import swiperTabHead from '../../components/index/swiper-tab-head.vue';
	import user from "../../components/user-list/user.vue"
	import loadMore from '../../components/common/load-more.vue';
	import noThing from '../../components/common/nothing.vue';

	export default {
		data() {
			return {
				swiperHeight: 500,
				tabIndex: 0,
				tabBars: [
					{
						name: "互关",
						id: "huguan",
						num: 10
					},
					{
						name: "关注",
						id: "guanzhu",
						num: 20
					},
					{
						name: "粉丝",
						id: "fensi",
						num: 30
					}
				],
				newsList: [
					{
						"loadtext": "上拉加载更多",
						list: [
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称3",
								"age": 20,
								"sex": 0,
								"isguanzhu": true
							},
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称4",
								"age": 20,
								"sex": 1,
								"isguanzhu": false
								
							}
						]
					},
					{
						"loadtext": "上拉加载更多",
						list: [
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称5",
								"age": 20,
								"sex": 0,
								"isguanzhu": true
							},
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称6",
								"age": 20,
								"sex": 1,
								"isguanzhu": false
								
							}
						]
					},
					{
						"loadtext": "上拉加载更多",
						list: [
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称1",
								"age": 20,
								"sex": 0,
								"isguanzhu": true
							},
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称2",
								"age": 20,
								"sex": 1,
								"isguanzhu": false
								
							}
						]
					}
				]
			}
		},
		methods: {
			/* 点击选项卡切换swiper组件 */
			tabtap(index){
				// console.log(index)
				this.tabIndex = index
			},
			/* 滑动swiper组件切换顶部选项卡 */
			tabChange(e){
				this.tabIndex = e.detail.current
			},
			/* 上拉触发触底事件 */
			loadmore(index){
				if(this.newsList[index].loadtext!=="上拉加载更多"){
					return;
				}
				this.newsList.loadtext="加载中"
				setTimeout(()=>{
					let obj = {
								"userpic": "../../static/image/head.jpg",
								"username": "昵称2",
								"age": 20,
								"sex": 1,
								"isguanzhu": false
								
							}
					this.newsList[index].list.push(obj)
					this.newsList[index].loadtext = "上拉加载更多"
				}, 1000)
			},
		},
		onNavigationBarButtonTap(e) {
			if(e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
			}
				
		},
		mounted(){
			/* 禁掉h5的放回按钮 */
			document.querySelector('.uni-page-head-hd').style.display = 'none'
		},
		components: {
			swiperTabHead,
			user,
			noThing,
			loadMore
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res)=>{
					let height = res.windowHeight-uni.upx2px(100)
					this.swiperHeight = height
				}
			})
		},
		
	}
</script>

<style lang="less" scoped>
	.body{
		padding: 0 20upx;
	}
	

</style>
