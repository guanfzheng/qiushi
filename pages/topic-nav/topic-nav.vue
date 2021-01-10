<template>
	<view>
		<swiper-tab-head
		:tabBars="tabBars" 
		:tabIndex="tabIndex"
		@tabtap="tabtap"></swiper-tab-head>
		
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
							<!-- 首页新闻信息卡片显示 -->
							<block v-for="(item, index) in news.list" :key="index">
								<topic-list :list="item"></topic-list>
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
	import swiperTabHead from "../../components/index/swiper-tab-head.vue"	
	import noThing from '../../components/common/nothing.vue';
	import loadMore from '../../components/common/load-more.vue';
	import topicList from '../../components/news/topic-list.vue';
	
	export default {
		data() {
			return {
				swiperHeight: 500,
				tabIndex: 0,
				tabBars: [
					{
						name: "关注",
						id: "guanzhu"
					},
					{
						name: "推荐",
						id: "tuijian"
					},
					{
						name: "体育",
						id: "tiyu"
					},
					{
						name: "热点",
						id: "redian"
					},
					{
						name: "财经",
						id: "caijing"
					},
					{
						name: "娱乐",
						id: "yule"
					}
				],
				newsList: [
					{
						loadtext: "上拉加载更多",
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
							},
							{
								"titlepic": "../../static/image/nothing.png",
								"title": "#话题名称#",
								"desc": "我是话题描述",
								"totalnum": 50,
								"todaynum": 10
							}
						]
					},
					{
						loadtext: "上拉加载更多",
						list:[
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
						]
					},
					{
						loadtext: "上拉加载更多",
						list:[
							{
								"titlepic": "../../static/image/nothing.png",
								"title": "#话题名称#",
								"desc": "我是话题描述",
								"totalnum": 50,
								"todaynum": 10
							}
						]
					},
					{
						loadtext: "上拉加载更多",
						list:[
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
							},
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
						]
					},
					{
						loadtext: "上拉加载更多",
						list:[]
					},
					{
						loadtext: "上拉加载更多",
						list:[
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
						]
					}
				],
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
			loadmore(index){
				if(this.newsList[index].loadtext!=="上拉加载更多"){
					return;
				}
				this.newsList.loadtext="加载中"
				setTimeout(()=>{
					let obj = {
						userpic: "../../static/image/head.jpg",
						username: "昵称1",
						isguanzhu: false,
						title: "我是标题1",
						type: "img",  //  img: 图片,video:视频
						titlepic: "../../static/image/index-list.jpg",
						playnum: "200000",
						long: "2:47",
						infonum: {
							index: 1, // 0:没有操作，1：顶，2踩
							dingnum: 11,
							cainum: 11
						},
						commentnum: 10,
						sharenum: 10
					}
					this.newsList[index].list.push(obj)
					this.newsList[index].loadtext = "上拉加载更多"
				}, 1000)
			},
		},
		components: {
			swiperTabHead,
			noThing,
			loadMore,
			topicList
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

<style>

</style>
