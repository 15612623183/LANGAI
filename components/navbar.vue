<template>
	<view>
		<view class="topline1">
			<u-popup v-model="show" mode="left" border-radius="14" length="30%">
				<view class="list">
					<button v-for='(item,index) in onedaylist'>{{item}}</button>
				</view>
			</u-popup>
			<view class="iconbackground1">
				<u-icon @click="show = true" color="#ffffff" name="list-dot" size="30"></u-icon>
			</view>
			<view class="iconbackground2">
				<text style="font-size: large;">LANGAI</text>
			</view>
			<view class="iconbackground1">
				<navigator url="/pages/search/search">
					<u-icon color="#ffffff" name="search" size="30"></u-icon>
				</navigator>
			</view>
		</view>
		<view class="topline2">
			<view class="iconbackground3">
				<u-icon color="#ffffff" name="calendar" size="30"></u-icon>
				<text>每日一花</text>
			</view>
			<view class="iconbackground3">
				<u-icon color="#ffffff" name="calendar" size="30"></u-icon>
				<text>朗爱推荐</text>
			</view>
			<view class="iconbackground3">
				<u-icon color="#ffffff" name="calendar" size="30"></u-icon>
				<text>我的关注</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "navbar",
		data() {
			return {
				show: false,
				onedaylist: ["吃饭", "睡觉", "背单词", "学习", "健身房", "B站", "闪动校园"]
			};
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">
	// .bg-color{
	// 	background-color: #000000;
	// }
	.list {
		height: 1334rpx;
		align-items: center; //子容器位置（居中）
		display: flex;
		flex-direction: column; //列排列
		justify-content: space-around; //排列方式
	}

	.topline1 {
		height: 130rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-around; //间距均等

		.iconbackground1 {
			margin-top: 40rpx;
			background-color: #ffd865;
			height: 90rpx;
			width: 90rpx;
			border-radius: 10rpx;

			.u-icon {
				margin: 30rpx;
			}
		}

		.iconbackground2 {
			margin-top: 40rpx;
			background-color: #ffd865;
			height: 90rpx;
			width: 500rpx;
			border-radius: 10rpx;
			text-align: center;

			text {
				line-height: 85rpx;
				font-weight: 800;
				color: #ffffff;
			}
		}
	}

	.topline2 {
		height: 100rpx;
		// margin-top:
		display: flex;
		flex-direction: row;
		justify-content: space-around;

		.iconbackground3 {
			margin-top: 10rpx;
			background-color: #92d050;
			height: 90rpx;
			width: 225rpx;
			border-radius: 10rpx;
			text-align: center;

			text {
				line-height: 85rpx;
				font-weight: 800;
				color: #ffffff;
			}
		}
	}
</style>
