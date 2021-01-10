<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	@import './common/uni.css';
	/* 加载字体图标 */
	@import './static/font/iconfont.css';
	/* 加载动画库 */
	@import './common/animate.css';
	/* 加载公共样式 */
	@import "./common/common.css";
</style>
