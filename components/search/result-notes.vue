<template>
	<view class="">
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
				<scroll-view :refresher-enabled="true" scroll-y class="notes_scroll">
					<view class="scroll">
						<view :style="{height:item.height+'rpx'}" class="images" v-for="(item,index) in choice3_leftimgs"
							:key="index">
							<image @click='gotodetails(index)' :src="item.src" mode="widthFix"></image>
						</view>
					</view>
					<view class="scroll">
						<view :style="{height:item.height+'rpx'}" class="images" v-for="(item,index) in choice3_rightimgs"
							:key="index">
							<image @click='gotodetails(index)' :src="item.src" mode="widthFix"></image>
						</view>
					</view>
				</scroll-view>
			</view>
			<view v-if="tabnumber === 1" class="user">
				user
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		name: 'result_notes',
		data() {
			return {
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
						src: '/static/picture/note1.png',
						height: '472'
					},
					{
						src: '/static/picture/note3.png',
						height: '519'
					},
					{
						src: '/static/picture/note1.png',
						height: '472'
					},
					{
						src: '/static/picture/note3.png',
						height: '519'
					},
				],
				choice3_rightimgs: [{
						src: '/static/picture/note2.png',
						height: '557'
					},
					{
						src: '/static/picture/note4.png',
						height: '535'
					},
					{
						src: '/static/picture/note2.png',
						height: '557'
					},
					{
						src: '/static/picture/note4.png',
						height: '535'
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
	
	.special_note{
		display: flex;
		justify-content: center;
		align-items: center;
		width: 170rpx;border-left: #dcdcdc solid 1rpx;
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
	.notes_scroll{
		height: 1039rpx;
		padding-top: 80rpx;
	}
	.scroll {
		width: 335rpx;
		display: inline-block;
		vertical-align: top;
		margin-left: 30rpx;
		margin-top: 10rpx;
	
		.images {
			margin-top: 20rpx;
			width: 375rpx;
	
			image {
				width: 335rpx;
			}
		}
	
	}
</style>
