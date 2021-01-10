<template>
	<view>
		<!-- topicInfo -->
		<topic-info :topicInfo="topicInfo"></topic-info>
		
		<swiper-tab-head
		:tabBars="tabBars" 
		:tabIndex="tabIndex"
		@tabtap="tabtap"
		scrollStyle="border-bottom:0;" 
		scrollItemStyle="width:50%;"></swiper-tab-head>
		
		<view class="topic-detail-list">
			<block v-for="(item, index) in followList" :key="index">
				<template v-if="tabIndex === index">
					<!-- 列表 -->
					<block v-for="(list, listIndex) in item.singleList" :key="listIndex">
						<common-list :item="list" :index="listIndex"></common-list>
					</block>
					<!-- 上拉加载 -->
					<load-more :loadtext="item.loadtext"></load-more>
				</template>
			</block>
		</view>
		
	</view>
</template>

<script>
	import topicInfo from "../../components/topic/topic-info.vue"	
	import swiperTabHead from '../../components/index/swiper-tab-head.vue';
	import commonList from "../../components/common/common-list.vue"
	import loadMore from "../../components/common/load-more.vue"
	export default {
		data() {
			return {
				"topicInfo": {
					"titlepic": "../../static/image/nothing.png",
					"title": "#话题名称#",
					"desc": "我是话题描述",
					"totalnum": 50,
					"todaynum": 10
				},
				tabIndex: 0,
				tabBars: [
					{
						name: "默认",
						id: "moren"
					},
					{
						name: "最新",
						id: "zuixin"
					}
				],
				/* 列表 */
				followList: [
					{
						loadtext: "上拉加载更多",
						singleList: [
							/* 默认 */
							{
								userpic: "../../static/image/head.jpg",
								username: "昵称1",
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
					{
						loadtext: "上拉加载更多",
						singleList: [
							/* 默认 */
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
				]
			}
		},
		methods: {
			/* 点击选项卡切换swiper组件 */
			tabtap(index){
				// console.log(index)
				this.tabIndex = index
			},
			/* 上拉触发触底事件 */
			loadmore(){
				if(this.followList[this.tabIndex].loadtext!=="上拉加载更多"){
					return;
				}
				this.followList[this.tabIndex].loadtext="加载中"
				setTimeout(()=>{
					let obj = {
								userpic: "../../static/image/head.jpg",
								username: "昵称1",
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
					this.followList[this.tabIndex].singleList.push(obj)
					this.followList[this.tabIndex].loadtext = "上拉加载更多"
				}, 1000)
			},
			/* 上拉刷新获取数据 */
			getData(){
				setTimeout(()=>{
					let arr = [
						{
							userpic: "../../static/image/head.jpg",
							username: "昵称dddd1",
							sex: 0 ,// 0:男，1女
							age: 25,
							isguanzhu: true,
							title: "我是标题ddddd",
							titlepic: "../../static/image/index-list.jpg",
							video: false,
							share: false,
							path: "深圳 龙岗",
							sharenum: 20,
							commentnum: 20,
							goodnum: 10
						},
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
						}
					]
					this.followList[this.tabIndex].singleList = arr 
					this.followList[this.tabIndex].loadtext = "上拉加载更多"
					uni.stopPullDownRefresh()
				}, 2000)
			}
		},
		components: {
			topicInfo,
			swiperTabHead,
			commonList,
			loadMore
		},
		/* 上拉触底事件 */
		onReachBottom(){
			this.loadmore()
		},
		/* 下拉刷新事件 */
		onPullDownRefresh() {
			this.getData()
		}
		
	}
</script>

<style lang="less" scoped>
	
</style>
