<template>
	<view class="mypage">
		<u-toast ref="uToast" />
		<view class="my_head">
			<!-- 头部背景-start -->
			<view class="head_background">
				<image :src="head_background" mode="widthFix"></image>
			</view>
			<!-- 头部背景-end -->
			<!-- 右上角按钮-start -->
			<view class="my_buttons">
				<view v-for="(item,index) in my_button" class="decorate_icon" @click="construction">
					<image :src="item" mode="widthFix"></image>
				</view>
			</view>
			<!-- 右上角按钮-end -->
			<!-- 个人主页信息-start -->
			<view class="personal_information">
				<view class="personal_main">
					<view class="personal_avatar">
						<image :src="personal.avatar" mode="widthFix"></image>
					</view>
					<view class="personal_identity">
						<view class="personal_up">
							<text style="font-size: 40rpx;">{{personal.name}}</text>
							<view class="level_icon">
								<text style="">{{personal.level}}</text>
							</view>

						</view>
						<view class="personal_middle">
							<image :src="personal.gender_icon" mode="widthFix"></image>
							<text>朗爱ID：{{personal.id}}</text>
							<image :src="personal.QR_code" mode="widthFix"></image>
						</view>
						<view class="personal_down">
							<image :src="personal.signature_icon" mode="widthFix"></image>
							<text>{{personal.signature}}</text>
						</view>
					</view>
				</view>
				<view class="personal_other">
					<view class="other_block">
						<text style="font-size: 30rpx;">{{personal.follows}}</text>
						<text style="font-size: 24rpx;">关注</text>
					</view>
					<view class="other_block">
						<text style="font-size: 30rpx;">{{personal.fans}}</text>
						<text style="font-size: 24rpx;">粉丝</text>
					</view>
					<view class="other_block">
						<text style="font-size: 30rpx;">{{personal.likes}}</text>
						<text style="font-size: 24rpx;">获赞</text>
					</view>
					<view class="other_block">
						<text style="font-size: 30rpx;">{{personal.coins}}</text>
						<text style="font-size: 24rpx;">朗币</text>
					</view>
				</view>
			</view>
			<!-- 个人主页信息-start -->
		</view>
		<view class="shortcut_block">
			<view v-for="(item,index) in shortcut_up" class="shortcut">
				<image :src="item.icon" mode="heightFix" @click="construction"></image>
				<text>{{item.name}}</text>
			</view>
		</view>
		<view class="shortcut_block">
			<view v-for="(item,index) in shortcut_middle" class="shortcut">
				<image :src="item.icon" mode="heightFix" @click="construction"></image>
				<text>{{item.name}}</text>
			</view>
		</view>
		<view class="shortcut_block">
			<view v-for="(item,index) in shortcut_down" class="shortcut">
				<image :src="item.icon" mode="heightFix" @click="construction"></image>
				<text>{{item.name}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'mypage',
		data() {
			return {
				shortcut_up: [{
					name: '识花记录',
					icon: '/static/icon/识花记录.png',
				}, {
					name: '我的笔记',
					icon: '/static/icon/笔记.png',
				}, {
					name: '我的消息',
					icon: '/static/icon/消息.png',
				}, {
					name: '我的课程',
					icon: '/static/icon/课程.png',
				}],
				shortcut_middle: [{
					name: '我的点赞',
					icon: '/static/icon/点赞.png',
				}, {
					name: '我的收藏',
					icon: '/static/icon/收藏.png',
				}, {
					name: '我的评论',
					icon: '/static/icon/评论.png',
				}, {
					name: '我的足迹',
					icon: '/static/icon/足迹.png',
				}],
				shortcut_down: [{
					name: '我的钱包',
					icon: '/static/icon/钱包.png',
				}, {
					name: '我的订单',
					icon: '/static/icon/订单.png',
				}, {
					name: '朗币中心',
					icon: '/static/icon/朗币中心.png',
				}, {
					name: '万物庄园',
					icon: '/static/icon/万物庄园.png',
				}],
				my_button: ["/static/icon/wd设置.png", "/static/icon/wd更多.png", "/static/icon/wd分享.png"],
				personal: {
					name: '知安',
					level: 'Lv1',
					gender_icon: '/static/icon/女.png',
					id: '23331218',
					QR_code: '/static/icon/二维码.png',
					signature_icon: '/static/icon/叶子个性签名.png',
					signature: '爱花草爱阳光爱世界万物~',
					avatar: '/static/icon/Avatar9.jpg',
					follows: 756,
					fans: 17,
					likes: 112,
					coins: 326,
				},
				head_background: "/static/picture/顶部波浪.png",
			}
		},
		methods: {
			construction() {
				this.$refs.uToast.show({
					title: '待开发中',
					type: 'warning',
					// url: '/pages/text/text'
				})
			}
		}
	}
</script>

<style lang="scss">
	.mypage {
		width: 750rpx;
		height: 1334rpx;
		background-color: #f5f5f5;
	}

	.my_head {
		height: 390rpx;
		border-radius: 0rpx 0rpx 30rpx 30rpx;
		background-color: #ffffff;
		box-shadow: 0rpx 0rpx 10rpx #e8e8e8;
	}

	.head_background {
		width: 750rpx;
		height: 390rpx;

		image {
			width: 100%;
		}
	}

	.my_buttons {
		height: 60rpx;
		width: 200rpx;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;
		margin-left: 510rpx;
		margin-top: -335rpx;

		.decorate_icon {
			position: relative;
			width: 60rpx;
			height: 60rpx;
			border-radius: 30rpx;
			display: flex;
			align-items: center;
			justify-content: center;
			background-color: #cca227;

			image {
				width: 40rpx;
			}
		}
	}

	.personal_identity {
		height: 300rpx;
		width: 750rpx;
	}


	.personal_main {
		margin-top: -20rpx;
		height: 145rpx;
		width: 750rpx;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;

		.personal_avatar {
			display: flex;
			justify-content: center;
			width: 205rpx;

			image {
				width: 145rpx;
				border-radius: 145rpx;
			}
		}

		.personal_identity {
			position: relative;
			height: 125rpx;
			width: 545rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-around;

			text {
				color: #ffffff;
			}

			.personal_up {
				height: 40rpx;
				display: flex;
				align-items: center;

				text {
					letter-spacing: 2rpx;
				}

				.level_icon {
					margin-top: 20rpx;
					margin-left: 15rpx;
					display: flex;
					justify-content: center;
					font-size: 24rpx;
					height: 25rpx;
					width: 55rpx;
					border-radius: 10rpx;
					color: #ffffff;
					border: #ffffff solid 2rpx;

					text {
						line-height: 20rpx;
						letter-spacing: 0rpx;
					}
				}
			}

			.personal_middle {
				height: 24rpx;
				display: flex;
				align-items: center;
				margin-left: -5rpx;

				image {
					width: 20rpx;
					margin-left: 5rpx;
				}

				text {
					margin-left: 5rpx;
					font-size: 24rpx;
					letter-spacing: 1rpx;
				}
			}

			.personal_down {
				height: 25rpx;
				display: flex;
				align-items: center;

				image {
					width: 25rpx;
				}

				text {
					font-size: 25rpx;
					margin-left: 5rpx;
					letter-spacing: 1rpx;
				}
			}
		}
	}

	.personal_other {
		width: 320rpx;
		height: 150rpx;
		padding-top: 55rpx;
		margin-left: 50rpx;
		position: relative;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		text-align: center;

		.other_block {
			height: 55rpx;
			display: flex;
			flex-direction: column;
			align-items: center;

			text {
				line-height: 30rpx;
				padding-bottom: 15rpx;
				color: #999999;
			}
		}
	}

	.shortcut_block {
		width: 690rpx;
		height: 220rpx;
		margin: 30rpx;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-around;
		background-color: #ffffff;
		border-radius: 30rpx;
		box-shadow: 0rpx 0rpx 10rpx #e8e8e8;

		.shortcut {
			height: 160rpx;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: space-around;

			image {
				height: 65rpx;
			}
		}
	}
</style>
