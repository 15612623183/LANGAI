<template>
	<view class="user">	
		<view v-for="(item,index) in user" class="user_block">
			<view>
				<image :src="item.avatar" mode="aspectFill" class="avatar"></image>
			</view>
			<!-- 用户信息-start -->
			<view class="information_box">
				<!-- 用户昵称-start -->
				<view class="nickname_box">
					<text>{{item.nickName}}</text>
				</view>
				<!-- 用户昵称-end -->
				<!-- 用户ID-start -->
				<view class="id_box">
					<text>LA ID：{{item.id}}</text>
				</view>
				<!-- 用户ID-end -->
			</view>
			<!-- 用户信息-end -->
			<!-- 关注按钮-start -->
			<view>
				<view class="follow"><text>关注</text></view>
			</view>
			<!-- 关注按钮-end -->
		</view>
		<u-divider half-width="50" fontSize="24">没有更多内容了哦</u-divider>
	</view>
</template>

<script>
	export default {
		name: 'result_user',
		data() {
			return {
				user: [{
					id: '379207252',
					nickName: '可爱的玩偶花束',
					avatar: '/static/picture/Avatar5.jpg',
				}, {
					id: '265628649',
					nickName: '小可爱花束',
					avatar: '/static/picture/Avatar7.jpg',
				}],
			}
		}
	}
</script>

<style lang="scss">
	.user {
		margin-top: 10rpx;
	}

	.user_block {
		width: 750rpx;
		padding: 20rpx 0rpx;
		display: flex;
		align-items: center;

		.avatar {
			margin-left: 35rpx;
			width: 100rpx;
			height: 100rpx;
			border-radius: 50%;
		}

		.information_box {
			margin-left: 20rpx;
			width: 470rpx;

			.id_box {
				text {
					font-size: 20rpx;
					color: #666666;
				}
			}

			.nickname_box {
				display: flex;

				text {
					font-size: 30rpx;
				}
			}
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
</style>
