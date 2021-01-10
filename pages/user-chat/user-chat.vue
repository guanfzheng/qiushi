<template>
	<view>
		
		<scroll-view id="scrollview" scroll-y 
		:scroll-top="scrollTop" 
		:scroll-with-animation="true"
		:style="{height:style.contentH+'px'}">
			<!-- 聊天列表 -->
			<block v-for="(item, index) in list" :key="index">
				<user-chat-list :item="item"></user-chat-list>
			</block>
		</scroll-view>
		
		
		<!-- 底部发送信息组件 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
		
	</view>
	
</template>

<script>
	import userChatBottom from "../../components/user-chat/user-chat-bottom.vue"
	import time from "../../common/time.js"
	import userChatList from "../../components/user-chat/user-chat-list.vue"
	export default {
		data() {
			return {
				list: [],
				scrollTop: 0,
				style: {
					contentH: 0,
					itemH: 0
				}
			}
			
		},
		methods: {
			submit(data){
				/* 构建数据 */
				let now = new Date().getTime()
				let mess = {
						"userpic": "../../static/image/head.jpg",
						"isme": true,
						"type": "text",
						"data": data ,
						"time": now,
						"gstime": time.gettime.getChatTime(now, this.list[this.list.length-1].time)
					}
				this.list.push(mess)
				this.pageToBottom()
			},
			/* 获取聊天数据 */
			getData(){
				let arr = [
					{
						"userpic": "../../static/image/head.jpg",
						"isme": true,
						"type": "img",
						"data": "../../static/image/index-list.jpg" ,
						"time": "1554970014",
						"gstime": "12:00"
					},
					{
						"userpic": "../../static/image/head.jpg",
						"isme": false,
						"type": "text",
						"data": "哈哈哈" ,
						"time": "1554970014",
						"gstime": "12:00"
					}
				]
				for(let i = 0 ; i < arr.length; i++)
				{
					arr[i].gstime = time.gettime.getChatTime(arr[i].time, i>0?arr[i-1].time:0)
				}
				this.list = arr
			},
			/* 初始化参数 */
			initData(){
				try {
					const res = uni.getSystemInfoSync();
					this.style.contentH=res.windowHeight - uni.upx2px(120);
				} catch (e) { }
			},
			/* 计算滑动高度 */
			pageToBottom(){
				let q = uni.createSelectorQuery()
				q.select("#scrollview").boundingClientRect() 
				q.selectAll(".user-chat-item").boundingClientRect()
				
				q.exec((res)=>{
					res[1].forEach((ret)=>{
						this.style.itemH += ret.height;
					});
					
					if(this.style.itemH > this.style.contentH){
						this.scrollTop=this.style.itemH;
					}
					
				})
			}
		},
		components: {
			userChatBottom,
			userChatList
		},
		onLoad(){
			this.getData()
			this.initData()
		},
		onReady() {
			this.pageToBottom()
		}
	}
</script>

<style lang="less" scoped>
	
	
</style>
