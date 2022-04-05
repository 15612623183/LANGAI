<template>
	<view class="">


		<view class="result_bar">
			<view @click="result_choose(index)" v-if="" class="classification_choice"
				v-for="(item,index) in result_classification" :key="index">
				<view style="display: flex;flex-direction: column;align-items: center;">
					<view :class="(tabnumber === index) ? 'word_active' : 'word'">
						<text>{{item}}</text>
					</view>
					<image v-if="tabnumber === index" :src="bottom_selection_icon" mode="widthFix"
						style="width: 40rpx;">
					</image>
				</view>
			</view>
		</view>
		<view class="search_result">
			<view v-if="tabnumber === 0" class="notes">
				<view class="notes_bar">
					<view @click="notes_choose(index)" class="notes_choice" v-for="(item,index) in notes_classification"
						:key="index">
						<view :class="(notesnum === index) ? 'word_active' : 'word'">
							<view v-if="index < 3" style="width: 100rpx;">
								<text>{{item}}</text>
							</view>
							<view v-else class="special_note">
								<text>{{item}}</text>
								<image v-if="index === 3 & index !== notesnum" :src="video_normal_icon"
									style="width: 26rpx;" mode="widthFix"></image>
								<image v-if="index === 3 & index === notesnum" :src="video_active_icon"
									style="width: 26rpx;" mode="widthFix"></image>
								<image v-if="index === 4 & index !== notesnum" :src="image_normal_icon"
									style="width: 26rpx;" mode="widthFix"></image>
								<image v-if="index === 4 & index === notesnum" :src="image_active_icon"
									style="width: 26rpx;" mode="widthFix"></image>
							</view>
						</view>
					</view>
				</view>
				<!-- 瀑布流主要内容 -->
				<scroll-view :refresher-enabled="true" :scroll-y="true" class="choice3_scroll">
					<view class="scroll">
						<view :style="{height:item.height+'rpx'}" class="images"
							v-for="(item,index) in choice3_leftimgs" :key="index">
							<image @click='gotodetails(index)' :src="item.src" mode="widthFix"></image>
						</view>
					</view>
					<view class="scroll">
						<view :style="{height:item.height+'rpx'}" class="images"
							v-for="(item,index) in choice3_rightimgs" :key="index">
							<image @click='gotodetails(index)' :src="item.src" mode="widthFix"></image>
						</view>
					</view>
				</scroll-view>
			</view>
			<view v-if="tabnumber === 1" class="user">

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
		</view>

	</view>
</template>

<script>
	export default {
		name: 'result_bar',
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
				result_classification: [
					"笔记",
					"用户",
				],
				notes_classification: [
					"全部",
					"热门",
					"最新",
					"视频",
					"图片",
				],
				bottom_selection_icon: '/static/icon/选择下标.png',
				video_normal_icon: '/static/icon/播放_normal.png',
				video_active_icon: '/static/icon/播放.png',
				image_normal_icon: '/static/icon/image_normal.png',
				image_active_icon: '/static/icon/image.png',
				tabnumber: 0,
				notesnum: 0,

				choice3_leftimgs: [{
						src: '/static/picture/1.png',
						height: '472'
					},
					{
						src: '/static/picture/3.png',
						height: '460'
					},
					{
						src: '/static/picture/1.png',
						height: '472'
					},
					{
						src: '/static/picture/3.png',
						height: '460'
					},
					{
						src: '/static/picture/1.png',
						height: '472'
					},
					{
						src: '/static/picture/3.png',
						height: '460'
					},
				],
				choice3_rightimgs: [{
						src: '/static/picture/2.png',
						height: '511'
					},
					{
						src: '/static/picture/4.png',
						height: '430'
					},
					{
						src: '/static/picture/2.png',
						height: '511'
					},
					{
						src: '/static/picture/4.png',
						height: '430'
					},
					{
						src: '/static/picture/2.png',
						height: '511'
					},
					{
						src: '/static/picture/4.png',
						height: '430'
					},
				],
			}
		},
		methods: {
			result_choose(index) {
				this.tabnumber = index;
				console.log('可爱花束' + this.tabnumber)
			},
			notes_choose(index) {
				this.notesnum = index;
				console.log('笔记' + this.notesnum)
			},
		},
	}
</script>

<style lang="scss">
	.word_active {
		display: flex;

		text {
			font-size: 24rpx;
			color: #000000;
		}

		image {
			margin-left: 20rpx;
		}
	}

	.word {

		text {
			font-size: 24rpx;
			color: #999999;
		}

		image {
			margin-left: 20rpx;
		}
	}

	.special_note {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 170rpx;
		border-left: #dcdcdc solid 1rpx;
	}

	.result_bar {
		margin-left: 280rpx;
		height: 45rpx;
		width: 190rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		background-color: #f5f5f5;

		.classification_choice {
			text-align: center;
		}
	}


	.notes_bar {
		position: fixed;
		z-index: 500;
		height: 80rpx;
		width: 750rpx;
		background-color: #f5f5f5;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
		border-bottom: #dcdcdc solid 1rpx;
	}

	.notes_choice {
		display: flex;
		flex-direction: row;
		align-items: center;
		text-align: center;
	}

	.scroll {
		width: 335rpx;
		display: inline-block;
		vertical-align: top;
		margin-top: 80rpx;
		margin-left: 30rpx;

		.images {
			margin-top: 20rpx;
			width: 375rpx;

			image {
				width: 335rpx;
			}
		}

	}

.user{
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
				text{
					font-size: 20rpx;
					color: #666666;
				}
			}

			.nickname_box {
				display: flex;
				text{
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
