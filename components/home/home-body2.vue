<template>
	<view style="background-color: #ffffff;height: 490rpx;padding-top: 210rpx;" class="">
		<view class="choice2_head">
			<swiper class="choice2_swiper" :indicator-dots="true" :autoplay="false" :interval="2000" :duration="500"
				indicator-active-color="#ffffff">
				<swiper-item>
					<view class="swiper-item">
						<image src="../../static/picture/儿童花艺_看图王.web.jpg" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item">
						<image src="../../static/picture/儿童花艺5_看图王.web.jpg" mode=""></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item">
						<image src="../../static/picture/Avatar7.jpg" mode=""></image>
					</view>
				</swiper-item>
			</swiper>
			<view class="Recommend_items">
				<view class="Recommend_item" v-for="(item,index) in Recommended_items" :key="index">
					<view class="item_image">
						<image :src="item.iconsrc" mode="widthFix" style="width: 80rpx;"></image>
					</view>
					<text>{{item.name}}</text>
				</view>
			</view>
		</view>
		<scroll-view class="choice2_body" :refresher-enabled="true" :scroll-y="true">
			<view v-for="(item,index) in Recommended_blocks" class="item_block">
				<image :src="item.picture" mode="widthFix"></image>
				<!-- <view class="title">
					<text>{{item.title}}</text>
				</view>
				<view class="Recommend_content">
					
				</view> -->
			</view>
			<view class="last_block">
				<image :src="last_block.picture" mode="widthFix"></image>
				<!-- <view class="title">
					<text>{{item.title}}</text>
				</view>
				<view class="Recommend_content">
					
				</view> -->
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		name: "home-body2",
		data() {
			return {
				Recommended_items: [{
					name: "认识植物",
					iconsrc: "/static/icon/1认识植物.png",
				}, {
					name: "书籍推荐",
					iconsrc: "/static/icon/1书籍推荐.png",
				}, {
					name: "朗爱学院",
					iconsrc: "/static/icon/1朗爱学院.png",
				}, {
					name: "知识彩蛋",
					iconsrc: "/static/icon/1知识彩蛋.png",
				}, {
					name: "趣味挑战",
					iconsrc: "/static/icon/1趣味挑战.png",
				}],
				Recommended_blocks: [{
					title: "每周推荐",
					picture: "../../static/picture/每周推荐.png"
				}, {
					title: "新书推荐",
					picture: "../../static/picture/新书推荐.png"
				}, {
					title: "热门课程",
					picture: "../../static/picture/热门课程.png"
				}, {
					title: "最新活动",
					picture: "../../static/picture/最新活动.png"
				}],
				last_block:{
					title: "心水好物",
					picture: "../../static/picture/心水好物.png"
				},
			};
		}
	}
</script>

<style lang="scss">
	.choice2_swiper {
		margin-left: 30rpx;
		height: 260rpx;
		width: 690rpx;
		padding-top: 40rpx;

		.swiper-item {
			height: 100%;
			border-radius: 50rpx;

			image {
				width: 690rpx;
				height: 260rpx;
				border-radius: 10rpx;
			}
		}

	}

	.Recommend_items {
		height: 190rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-around;

		.Recommend_item {
			height: 195rpx;
			width: 100rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-around;

			.item_image {
				margin-left: 10rpx;
				margin-top: 40rpx;
				height: 80rpx;
				width: 80rpx;
				border-radius: 40rpx;
				background-color: #e6534e;
				text-align: center;
			}
			text {
				font-size: 25rpx;
				line-height: 75rpx;
			}
		}
	}
	
	.choice2_head{
		width: 750rpx;
		background-color: #ffffff;
		position: fixed;
		z-index: 500;
	}
	
	.choice2_body{
		margin-top: 500rpx;
		height: 500rpx;
		background-color: #f5f5f5;
		.item_block{
		width: 706rpx;
		height: 349rpx;
		margin-top: 70rpx;
		margin-left: 30rpx;
		image{
			width: 100%;
		}
	}
	}
	
	.last_block{
		width: 728rpx;
		height: 551rpx;
		margin-top: 70rpx;
		margin-left: 30rpx;
		image{
			width: 100%;
		}
	}
	
</style>
