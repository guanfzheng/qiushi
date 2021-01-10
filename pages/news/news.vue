<template>
	<view>
		<!-- 自定义导航 -->
		<news-nav-bar :tabBars="tabBars" :tabIndex="tabIndex" @changeTab="changeTab"></news-nav-bar>
		
		<!-- 列表 -->
		<!-- <block v-for="(item, index) in list" :key="index">
			<common-list :item="item" :index="index" @guanzhu="guanzhu(index)" @quguan="quguan(index)"></common-list>
		</block> -->
		
		<view class="uni-tab-bar">
			<swiper 
			class="swiper-box" 
			:style="{height:swiperHeight+'px'}"
			:current="tabIndex"
			@change="tabChange">
				<!-- 关注 -->
				<swiper-item>
					<scroll-view scroll-y class="list" 
				@scrolltolower="loadmore()">
						<template v-if="followList.singleList.length>0">	
							<block v-for="(item, index) in followList.singleList" :key="index">
								<common-list :item="item" :index="index" @guanzhu="guanzhu(index)" @quguan="quguan(index)"></common-list>
							</block>
							<load-more :loadtext="followList.loadtext"></load-more>
						</template>
						<template v-else>
							<no-thing></no-thing>
						</template>
					</scroll-view>
				</swiper-item>
				<!-- 话题 -->
				<swiper-item>
					<scroll-view scroll-y class="list">
						<!-- 搜索框 -->
						<view class="search-input">
							<input class="uni-input" 
							placeholder="搜索内容"
							placeholder-class="icon iconfont icon-sousuo topic-search"/>
						</view>
						<!-- 轮播图 -->
						<swiper class="topic-swiper" 
						:indicator-dots="true" 
						:autoplay="true" 
						:interval="3000" 
						:duration="1000">
							<block v-for="(image, index) in topic.swiper" 
								:key="index">
								<swiper-item>
									<image 
									:src="image.img" 
									mode="widthFix"
									lazy-load></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<topic-nav :nav="topic.nav"></topic-nav>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view>最近更新</view>
							<block v-for="(item, index) in topic.list" :key="index">
								<topic-list :list="item"></topic-list>
							</block>
						</view>	
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
		
		
		
		
	</view>
</template>

<script>
	import newsNavBar from "../../components/news/news-nav-bar.vue";
	import commonList from "../../components/common/common-list.vue";
	import loadMore from "../../components/common/load-more.vue"
	import noThing from "../../components/common/nothing.vue"
	import topicNav from "../../components/news/topic-nav.vue"
	import topicList from "../../components/news/topic-list.vue"
	export default {
		data() {
			return {
				swiperHeight: 500,
				tabIndex: 0,
				tabBars: [
					{
						"name": "关注",
						"id": "guanzhu"
					},
					{
						"name": "话题",
						"id": "huati"
					}
				],
				/* 列表 */
				followList: {
					loadtext: "上拉加载更多",
					singleList: [
						/* 图文 */
						{
							userpic: "../../static/image/head.jpg",
							username: "昵称",
							sex: 0 ,// 0:男，1女
							age: 25,
							isguanzhu: true,
							title: "我是标题",
							titlepic: "../../static/image/index-list.jpg",
							video: false,
							share: false,
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 20,
							goodnum: 10
						},
						/* 视频 */
						{
							userpic: "../../static/image/head.jpg",
							username: "昵称",
							sex: 1 ,// 0:男，1女
							age: 25,
							isguanzhu: false,
							title: "我是标题",
							titlepic: "../../static/image/index-list.jpg",
							video: {
								looknum: "20w",
								long: "2:47"
							},
							share: false,
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 20,
							goodnum: 10
						},
						/* 分享 */
						{
							userpic: "../../static/image/head.jpg",
							username: "昵称",
							sex: 0 ,// 0:男，1女
							age: 25,
							isguanzhu: false,
							title: "我是标题",
							titlepic: "",
							video: false,
							share: {
								title: "我是标题",
								titlepic: "../../static/image/index-list.jpg"
							},
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 20,
							goodnum: 10
						}
					]
				},
				/* 话题 */
				/* swiper */
				topic: {
					swiper: [
						{
							"img": "../../static/image/index-list.jpg"
						},
						{
							"img": "../../static/image/index-list.jpg"
						},
						{
							"img": "../../static/image/index-list.jpg"
						}
					],
					nav: [
						{
							"name": "最新"
						},
						{
							"name": "游戏"
						},
						{
							"name": "打卡"
						},
						{
							"name": "情感"
						},
						{
							"name": "故事"
						},
						{
							"name": "最爱"
						}
						
					],
					list: [
						{
							"titlepic": "../../static/image/nothing.png",
							"title": "#话题名称#",
							"desc": "我是话题描述",
							"totalnum": 50,
							"todaynum": 10
						},
						{
							"titlepic": "../../static/image/nothing.png",
							"title": "#话题名称1#",
							"desc": "我是话题描述1",
							"totalnum": 23,
							"todaynum": 5
						}
					],
					
				}
				
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res)=>{
					let height = res.windowHeight-uni.upx2px(100)
					this.swiperHeight = height
					console.log(this.swiperHeight)
				}
			})
		},
		methods: {
			
			/* 更改tabBar */
			changeTab(index){
				this.tabIndex = index
			},
			/* 关注 */
			guanzhu(index){
				this.followList.singleList[index].isguanzhu = true
			},
			/* 取关 */
			quguan(index){
				this.followList.singleList[index].isguanzhu = false
			},
			/* 上拉触发触底事件 */
			loadmore(){
				if(this.followList.loadtext!=="上拉加载更多"){
					return;
				}
				this.followList.loadtext="加载中"
				setTimeout(()=>{
					let obj = {
							userpic: "../../static/image/head.jpg",
							username: "昵称",
							sex: 0 ,// 0:男，1女
							age: 25,
							isguanzhu: true,
							title: "我是标题",
							titlepic: "../../static/image/index-list.jpg",
							video: false,
							share: false,
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 20,
							goodnum: 10
						}
					this.followList.singleList.push(obj)
					this.followList.loadtext = "上拉加载更多"
				}, 1000)
			},
			tabChange(e){
				this.tabIndex = e.detail.current
			}
			
		},
		components:{
			newsNavBar,
			commonList,
			loadMore,
			noThing,
			topicNav,
			topicList
		}
	}
</script>

<style lang="less" scoped>

	/* 话题 */
	.search-input{
		padding: 20upx;
		
		&>input{
			background-color: #F4F4F4;
			border-radius: 10upx;
		}
		
		.topic-search{
			display: flex;
			justify-content: center;
			align-items: center;
			font-size: 27upx;
		}
	}
	.topic-swiper{
		padding: 0 20upx 20upx 20upx;
		
		image{
			width: 100%;		
			border-radius: 10upx;
		}
	}
	
	.topic-new{
		padding: 20upx;
		&>view:first-child{
			padding-bottom: 10upx;
			font-size: 32upx;
		}
	}
</style>
