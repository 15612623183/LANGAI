<template>
	<view>
		<!-- 导航栏 -->
		<view class="detail_head">
			<view class="detailblock">
				<view class="back_icon">
					<u-icon class="uicon" name="/static/icon/back.png" size="22rpx" @click="goback"></u-icon>
				</view>
				<view class="inputblock">
					<image src="/static/picture/Avatar1.jpg" mode="widthFix" style="width: 80rpx;border-radius: 40rpx;">
					</image>
					<text style="margin-left: 30rpx;">花园宝妈</text>
				</view>
				<view>
					<view class="follow"><text>关注</text></view>
				</view>
				<view class="back_icon">
					<u-icon class="uicon" name="heart" color="#dd5050" size="30rpx" @click="goback"></u-icon>
				</view>
			</view>
		</view>
		<scroll-view class="detail_body" scroll-y>
			<view class="detail_swiper">
				<swiper style="margin-left: 30rpx;margin-top: 30rpx;width: 690rpx;height: 750rpx;" indicator-active-color="#dd5050"
					indicator-color="#cccccc" :indicator-dots="true" :autoplay="false" :interval="3000"
					:duration="1000" @change="numchange($event.detail.current)">
					<swiper-item>
						
						<view class="swiper-item">
							<image src="@/static/picture/XHS_1648287101821b3497c52-ee7e-3955-a0a2-67671d4a.jpg" mode="">
							</image>
						</view>
					</swiper-item>
					<swiper-item>
						<view class="swiper-item">
							<image src="../../static/picture/儿童花艺7_看图王.jpg" mode=""></image>
						</view>
					</swiper-item>
				</swiper>
				<view class="item_num">
							<text>{{dotnum}}/2</text>
						</view>
			</view>
			<view class="blogger_content">
				<text style="font-size: 35rpx;font-weight: 600;">{{blogger_word.title}}</text>
				<text style="font-size: 30rpx;">{{blogger_word.text}}</text>
				<text style="font-size: 30rpx;color: #65abd7;">{{blogger_word.talk}}</text>
				<text style="font-size: 28rpx;color: #666666;">{{blogger_word.at}}</text>
			</view>
			<view class="release_date">
				<text style="font-size: 25rpx;color: #999999;">{{blogger_word.time}}</text>
			</view>
			<view class="comment" style="height: 800rpx;">
				<comments></comments>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import comments from '@/components/comments.vue'
	export default {
		data() {
			return {
				dotnum:1,
				blogger_word:{
					title:'超轻黏土|| 送你一束永不凋谢的花\n',
					text:'超轻黏土花束第一束联系打卡\n送给孩子的生日花束\n愿你健康快乐成长\n',
					talk:'#超轻黏土 #DIY手工制作 #我的手工日常\n',
					at:'@玛卡·巴卡\n',
					time:'昨天19:16\n',
				},
			}
		},
		methods: {
			//返回主页
			goback() {
				uni.navigateBack({})
			},
			numchange(event){
				this.dotnum = event+1;
				console.log(this.dotnum);
			}
		},
		components:{
			comments,
		},
	}
</script>

<style lang="scss" scoped>
	/deep/ .uni-swiper-dot{
		width: 10rpx;
		height: 10rpx;
	}
	
	.detail_head {
		background-color: #f0d9f0;
		height: 170rpx;
		border-radius: 0rpx 0rpx 30rpx 30rpx;
		display: flex;
		//position: fixed;

		.detailblock {
			margin-top: 70rpx;
			height: 80rpx;
			display: flex;
			flex-direction: row;
			align-items: center;

			.back_icon {
				width: 80rpx;

				.uicon {
					margin-left: 30rpx;
				}
			}

			.inputblock {
				width: 470rpx;
				height: 60rpx;
				display: flex;
				flex-direction: row;
				align-items: center;
			}

			.follow {
				height: 50rpx;
				width: 90rpx;
				text-align: center;
				align-items: center;
				color: #dd5050;
				border: #dd5050;
				border-radius: 25rpx;
				border-style: solid; //实线边框

				text {
					font-size: 25rpx;
				}
			}
		}
	}
	
	.detail_body{
		height: 1164rpx;
	}
	
	.detail_swiper {
		height: 750rpx;
		width: 750rpx;
		
		.swiper-item {
			image {
				width: 690rpx;
				height: 700rpx;
				border-radius: 35rpx;
			}
		}
		
		.item_num{
			position:absolute;
			width: 70rpx;
			height: 50rpx;
			margin-left: 635rpx;
			margin-top: -730rpx;
			background-color: #666666;
			display: flex;
			justify-content: center;
			align-items: center;
			border-style: solid;
			border-color: #666666;
			border-radius: 25rpx;
			text{
				color: #ffffff;
				font-size: 27rpx;
				line-height: 25rpx;
			}
		}
	}
	
	.blogger_content{
		height: 300rpx;
		width: 690rpx;
		margin-left: 30rpx;
		text{
			line-height: 50rpx;
		}
	}
	.release_date{
		display: flex;
		align-items: center;
		height: 120rpx;
		width: 690rpx;
		margin-left: 30rpx;
		border-bottom-style: solid;
		border-bottom-color: #dddcdc;
	}
</style>
