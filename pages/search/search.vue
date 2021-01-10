<template>
	<view>
		<template v-if="list.length>0">
			<block v-for="(item, index) in list">
				<index-list :item="item" :index="index"></index-list>
			</block>
			<load-more :loadtext="loadtext"></load-more>
		</template>
		<template v-else-if="isSearch && list.length<1">
			<no-thing></no-thing>
		</template>
	</view>
</template>

<script>
	import indexList from "../../components/index/index-list.vue"
	import loadMore from '../../components/common/load-more.vue';
	import noThing from '../../components/common/nothing.vue';
	export default {
		data() {
			return {
				loadtext: "上拉加载更多",
				isSearch: false,
				list:[],
				searchText:""
			}
		},
		methods: {
			/* 上拉触发触底事件 */
			loadmore(){
				if(this.loadtext!=="上拉加载更多"){
					return;
				}
				this.loadtext="加载中"
				setTimeout(()=>{
					let obj = {
						userpic: "../../static/image/head.jpg",
						username: "昵称2",
						isguanzhu: true,
						title: "我是标题2",
						type: "video",  //  img: 图片,video:视频
						titlepic: "../../static/image/index-list.jpg",
						playnum: "200000",
						long: "2:47",
						infonum: {
							index: 2, // 0:没有操作，1：顶，2踩
							dingnum: 11,
							cainum: 11
						},
						commentnum: 15,
						sharenum: 20
					}
					this.list.push(obj)
					this.loadtext = "上拉加载更多"
				}, 1000)
			},
			/* 搜索功能 */
			getData(){
				uni.showLoading()
				setTimeout( ()=>{
					let arr = [
					{
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
					},
					{
						userpic: "../../static/image/head.jpg",
						username: "昵称3",
						isguanzhu: true,
						title: "我是标题2",
						type: "video",  //  img: 图片,video:视频
						titlepic: "../../static/image/index-list.jpg",
						playnum: "200000",
						long: "2:47",
						infonum: {
							index: 2, // 0:没有操作，1：顶，2踩
							dingnum: 11,
							cainum: 11
						},
						commentnum: 15,
						sharenum: 20
					}
				]
				this.list = arr
				uni.hideLoading()
				this.isSearch = true
				},1000)
			}
		},
		mounted(){
			/* 禁掉h5的放回按钮 */
			document.querySelector('.uni-page-head-hd').style.display = 'none'
		},
		/* 监听标题按钮的原生点击事件 */
		onNavigationBarButtonTap(e){
			if(e.index === 0)
			{
				 uni.navigateBack({
				 	delta: 1
				 })
			}
		},
		/* 监听原生标题栏搜索输入框输入内容变化事件 */
		onNavigationBarSearchInputChanged(e){
			this.searchText = e.text
		},
		/* 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。 */
		onNavigationBarSearchInputConfirmed(e){
			if(e.text){
				this.getData()
			}
		},
		components: {
			indexList,
			noThing,
			loadMore
		},
		onReachBottom() {
			this.loadmore()
		},
		onPullDownRefresh() {
			this.getData()
			uni.stopPullDownRefresh()
		}
		
	}
</script>

<style>

</style>
