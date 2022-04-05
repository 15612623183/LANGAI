<template>
	<view style="height: 210rpx;position: fixed;z-index: 500;">
		<u-toast ref="uToast" />
		<view class="homehead_background">
			<image :src="picsrc" mode="">
			</image>
		</view>
		<view class="homehead_top">
			<view class="decorate_icon" @click="developing">
				<image :src="icon_more" mode="widthFix"></image>
			</view>
			<view class="checkin" @click="developing">
				<text>签 到</text>
			</view>
			<view class="decorate_icon" @click="gotosearch">
				<image :src="icon_search" mode="widthFix"></image>
			</view>
		</view>
		<view class="homehead_bottom">
			<view @click="choose(index)" class="decorate_icon" v-for="(item,index) in choices" :key="index">
				<view v-if="choice === index" style="display: flex;align-items: center;">
					<image :src="item.factionicon_active" mode="heightFix"></image>
					<text style="font-weight: 500;color: #000000;line-height: 40rpx;">{{item.name}}</text>
				</view>
				<view v-else style="display: flex;align-items: center;">
					<image :src="item.factionicon" mode="heightFix"></image>
					<text style="line-height: 40rpx;">{{item.name}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "home-head",
		data() {
			return {
				choice: 1,
				choices: [{
					factionicon: "/static/icon/choice1.png",
					factionicon_active: "/static/icon/choice1.png",
					name: "每日花签",
				}, {
					factionicon: "/static/icon/choice2.png",
					factionicon_active: "/static/icon/choice2_active.png",
					name: "朗爱推荐",
				}, {
					factionicon: "/static/icon/choice3.png",
					factionicon_active: "/static/icon/花友日常.png",
					name: "花友日常",
				}],
				icon_more: "/static/icon/更多.png",
				icon_search: "/static/icon/搜索.png",
				picsrc: "/static/picture/homehead_background.png",
			};
		},
		methods: {
			developing() {
				this.$refs.uToast.show({
					title: '待开发中',
					type: 'warning',
					// url: '/pages/text/text'
				})
			},
			choose(index) {
				if (index === this.choice) {
					return;
				}
				this.choice = index;
				this.$emit("choose", index)
				console.log(index);
			},
			gotosearch() {
				uni.navigateTo({
					url: '/pages/search/search'
				})
			}
		}
	}
</script>

<style lang="scss">
	.homehead_background {
		width: 750rpx;
		height: 210rpx;

		image {
			width: 100%;
			height: 100%;
		}
	}

	.homehead_top {
		height: 60rpx;
		width: 630rpx;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;
		margin-left: 60rpx;
		margin-top: -155rpx;

		.decorate_icon {
			position: relative;
			width: 70rpx;
			display: flex;
			align-items: center;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.checkin {
			position: relative;
			height: 60rpx;
			width: 400rpx;
			background-color: #ffe7a0;
			text-align: center;
			border-radius: 30rpx;

			text {
				line-height: 60rpx;
				color: #603315;
				font-size: 30rpx;
				font-weight: 700;
			}
		}
	}

	.homehead_bottom {
		height: 95rpx;
		width: 700rpx;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-around;
		margin-top: 0rpx;
		margin-left: 25rpx;

		.decorate_icon {
			position: relative;
			height: 60rpx;
			width: 200rpx;
			display: flex;
			flex-direction: row;
			align-items: center;
			text-align: center;
			justify-content: space-around;

			image {
				height: 40rpx;
			}

			text {
				color: #666666;
				line-height: 35rpx;
			}
		}
	}
</style>
