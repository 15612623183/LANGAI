<template>
	<view>
	<view class="start">
		<swiper :indicator-dots="true" :autoplay="true" :duration="1000" :circular="false" indicator-active-color="#e6bc40">
			<swiper-item>
				<view class="skip">
					<u-button @click="gotohome" color="#999999":plain="true" size="mini" shape="circle">跳过</u-button>	
				</view>	
				<image mode="scaleToFill" src="/static/icon/lead1.png"></image>
			</swiper-item>
			<swiper-item>
				<view class="skip">
					<u-button @click="gotohome" color="#999999":plain="true" size="mini" shape="circle">跳过</u-button>	
				</view>	
				<image src="/static/icon/lead2.png"></image>
			</swiper-item>
			<swiper-item>
				<view class="skip">	</view>
				<image @click="gotohome" src="/static/icon/lead3.png"></image>
			</swiper-item>
		</swiper>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			gotohome(){
				uni.switchTab({
					url:"/pages/home/home"
				})
			}
		}
	}
</script>

<style lang="scss">
.start{
	swiper{
		width: 750rpx;
		height: 1334rpx;
		image{
			width: 100%;
			height: 89%;
		}
		background-color: #f5f5f5;
	}
.skip{
	height: 50rpx;
	width: 10%;
	background-color: #f5f5f5;
	padding-top: 64rpx;
	padding-left: 630rpx;
}
}
</style>
