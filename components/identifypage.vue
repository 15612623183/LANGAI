<template>
	<view>
		<view>
			<view>
				<navbar></navbar>
			</view>
			<view class="img-data">
				<u-upload
				    width="400" 
					height="400" 
					ref="uUpload" 
					:action="action" 
					:auto-upload="true" 
					name="image"
					max-count="1">
				</u-upload>
				<view class="resdata">
					<view v-for="(item,index) in resdata" :key="index">
						<text>{{item.name}}:</text>
						<text>{{parseFloat(item.score).toFixed(4)*100}}%</text>
					</view>	
				</view>
			</view>
			<u-button @click="identity">鉴别</u-button>
		</view>
	</view>
</template>

<script>
	import navbar from '../components/navbar.vue'
	export default {
		name:"identifypage",
		components: {
			navbar,
		},
		data() {
			return {
				current: 4,
				action: 'http://39.103.136.247:5088/api/image',
				resdata: [],
			}
		},
		methods: {
			identity() {
				this.$refs.uUpload.upload();
				setTimeout(() => {
					this.resdata = this.$refs.uUpload.lists[0].response.result //得到识别信息
				}, 1000) //等待上传
					// setTimeout(() => {
					// 	// JSON.parse 转成javascript的object对象
					// 	resolve(JSON.parse(res.data))
					// }, 1000)
			},
			postimg() {
				uni.chooseImage({
					count: 1, //图片数
					sizeType: ['compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['camera', 'album'], //相机或相册选择
					success: res => {
						this.imagepath = res.tempFilePaths
					}
				})
			},
			onShow() {
				uni.hideTabBar({
					animation: false
				})
			},
			onLoad() {
				this.tabbar
			}
		},
	}
</script>

<style lang='scss'>
	.img-data {
		display: flex;
		flex-direction: row;
		align-items: center;
		.resdata{
			height: 350rpx;
			width: 350rpx;
		}
	}
</style>
