<template>
	<view class="body">
		<!-- 操作列表 -->
		<paper-left-popup :show="show" @hide="hidepopup" @addfirend="addfriend" @clear="clear"></paper-left-popup>
		
		<!-- 小纸条列表 -->
		<block v-for="(item, index) in paperList" :key="index">
			<paper-list :paper="item"></paper-list>
		</block>
		
		<load-more :loadtext="loadtext"></load-more>
	</view>
</template>

<script>
	import paperList from "../../components/paper/paper-list.vue"
	import loadMore from '../../components/common/load-more.vue';
	import paperLeftPopup from "../../components/paper/paper-left-popup.vue"
	export default {
		data() {
			return {
				show: false,
				loadtext: "上拉加载更多",
				paperList: [
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "123",
					},
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "0",
					},
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "123",
					},
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "0",
					},
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "0",
					},
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "0",
					},
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "123",
					},
					{
						"userpic": "../../static/image/head.jpg",
						"username": "昵称",
						"time": "10:21",
						"data": "我是信息",
						"noreadnum": "0",
					}
				]
			}
		},
		methods: {
			getData(){
				
				setTimeout(()=> {
					let arr = [
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称1",
								"time": "10:21",
								"data": "我是信息",
								"noreadnum": "3",
							},
							{
								"userpic": "../../static/image/head.jpg",
								"username": "昵称2",
								"time": "10:21",
								"data": "我是信息",
								"noreadnum": "1",
							}
						]
					this.paperList = arr
			
				}, 1000)
			uni.stopPullDownRefresh()
			},
			/* 上拉触发触底事件 */
			loadmore(){
				if(this.loadtext!=="上拉加载更多"){
					return;
				}
				this.loadtext="加载中"
				setTimeout(()=>{
					let obj = {
								"userpic": "../../static/image/head.jpg",
								"username": "昵称2",
								"time": "10:21",
								"data": "我是信息",
								"noreadnum": "1",
							}
					this.paperList.push(obj)
					this.loadtext = "上拉加载更多"
				}, 1000)
			},
			/* 操作菜单 */
			addfriend(){
				console.log("加糗友")
				this.hidepopup()
			},
			clear(){
				console.log("清除缓存")
				this.hidepopup()
			},
			hidepopup(){
				this.show = false
			},
			showpopup(){
				this.show = true
			}
			
		},
		components:{
			paperList,
			loadMore,
			paperLeftPopup
		},
		/* 监听下拉刷新 */
		onPullDownRefresh() {
			this.getData()
				
		},
		onReachBottom(){
			this.loadmore()
		},
		onNavigationBarButtonTap(e) {
			if(e.index === 0){
				uni.navigateTo({
					url: "../user-list/user-list"
				})
			} else if(e.index === 1){
				this.showpopup()
			}
		}
	}
</script>

<style lang="less" scoped>
	.body{
		padding: 0 20upx;
		
	}
	
</style>
