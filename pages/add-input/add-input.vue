<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar 
		:statusBar="true" 
		rightText="发布" 
		left-icon="back" 
		@clickLeft="back" 
		@clickRight="summit">
			<view class="u-f u-f-ajc" style="flex: 1;" @tap="changelook">
				<text>{{yinsi}}</text>
				<text class="icon iconfont icon-xiala"></text>
			</view>
		</uni-nav-bar>
		
		<!-- 文本域 -->
		<view class="uni-textarea">
			<textarea v-model="text" placeholder="说一句话吧..." />
		</view>
		<!-- 上传多图功能 -->
		<upload-image @uploadImgList="uploadImgList"></upload-image>
		<!-- 弹出层Popup -->
		<uni-popup ref="popup" type="center">
		    <view class="popup">
		    	<image 
				src="../../static/image/add-input.png" 
				mode="widthFix"></image>
				<view>
					<view class="popup-text">1、涉及黄色，政治，广告及骚扰信息</view>
					<view class="popup-text">2、涉及人身攻击</view>
					<view class="popup-text">3、留联系方式，透露他人隐私</view>
					<view class="popup-text">一经核实将被封禁，情节严重者永久封禁</view>
					<button @tap="hidePopup">朕知道了</button>
				</view>
		    </view>
		</uni-popup>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue";
	import uploadImage from '../../components/common/upload-image.vue';
	import uniPopup from '@/components/uni-popup/uni-popup.vue';
	import uniPopupMessage from '@/components/uni-popup/uni-popup-message.vue';
	import uniPopupDialog from '@/components/uni-popup/uni-popup-dialog.vue';

	
	export default {
		data() {
			return {
				yinsi: "所有人可见",
				text: '',
				imgList: [],
				isQuit: false //是否退出
			}
		},
		onBackPress() {
			/* 判断text和imaList是否有值如果有值则询问是否保存，没有值则直接退出*/
			if(this.text === '' && this.imgList.length<1) {
				return ;
			}
			if(!this.isQuit){
				uni.showModal({
					content: "是否要保存为草稿？",
					cancelText: "不保存",
					confirmText: "保存",
					success:(res) => {
						if(res.confirm){
							console.log("保存")
						}else{
							console.log("不保存")
						}
						this.isQuit = true
						uni.navigateBack({
							delta: 1
						})
					}
				})
				return true;
			}
			
		},
		mounted() {
			this.$refs.popup.open()	
		},
		methods: {
			back(){
				uni.navigateBack({
					delta:1
				})
			},
			summit(){
				console.log("s")
			},
			changelook(){
				uni.showActionSheet({
					itemList:["所有人可见", "仅自己可见"],
					success:(res)=>{
						if(res.tapIndex === 0){
							this.yinsi = "所有人可见"
						}else if(res.tapIndex === 1){
							this.yinsi = "仅自己可见"
						}
					},
					fail:(res) =>{
						console.log(res.errMsg)
					},
				})
			},
			/* 更新数据 */
			uploadImgList(imageList){
				this.imgList = imageList
			},
			hidePopup(){
				this.$refs.popup.close()
			}
		},
		components:{
			uniNavBar,
			uploadImage,
			uniPopup,
			uniPopupMessage,
			uniPopupDialog
		}
	}
</script>

<style lang="less" scoped>
	.uni-textarea{
		border: 1upx solid #EEEEEE;
	}
	.popup{
		width: 600upx;
		background-color: #FFFFFF;
		border-radius: 10upx;
		margin: auto;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		
		image{
			width: 60%;
		}
		button{
			margin: 20upx;
			background-color: #FFE934;
			color: #FFFFFF;
		}
	}
</style>
