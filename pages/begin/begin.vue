<template>
	<view>
		<image class="imagesize" src="/static/icon/begin.png" mode="widthFix"></image>
	</view>
<!-- 	<u-transition :show="show" mode="zoom-in">
	        <view class="transition"></view>
	</u-transition> -->
</template>

<script>
	export default {
		data() {
			return {
				// show: true
			}
		},
		methods: {

		},
		onLoad(){
			let timer=setTimeout(()=>{
				clearTimeout(timer)
				uni.navigateTo({
					url:'/pages/start/start'
				})
			},4000)
		},
	}
</script>

<style>
.imagesize{
	width: 750rpx;
	height: 1334rpx;
}
</style>
