<template>
	<view style="background-color: #f5f5f5;" class="">
		
		<!-- 标签选择栏 -->
		<view class="choice3_tabs">
			<view @click="choose(index)" v-if="" class="choice3_tabs_word" v-for="(item,index) in choice3tabs"
				:key="index">
				<view v-if="tabnumber === index" style="display: flex;flex-direction: column;align-items: center;padding-top: 7rpx;">
					<text style="color: #000000;font-weight: 500;">{{item}}</text>
					<image src="/static/icon/选择下标.png" mode="widthFix" style="width: 36rpx;"></image>
				</view>
				<view v-else><text>{{item}}</text></view>
			</view>
		</view>
		<!-- 更多标签按钮 -->
		<view class="tabs_more" @click="developing">
			<u-icon name="arrow-down" color="#666666" size="28"></u-icon>
			<u-toast ref="uToast" />
		</view>
		
		<!-- 瀑布流主要内容 -->
		<scroll-view :refresher-enabled="true" :scroll-y="true" class="choice3_scroll">
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
</template>

<script>
	export default {
		name: "home-body3",
		data() {
			return {
				choice3tabs: [
					"全部",
					"户外赏花",
					"附近的人",
					"摄影",
					"多肉",
					"种植养护",
					" "
				],
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
				/* choice3_leftimgs: [{
						src: '/static/picture/XHS_1648287101821b3497c52-ee7e-3955-a0a2-67671d4a.jpg',
						bgcolor: ' #f0d9f0;'
					},
					{
						src: "/static/picture/Screenshot_2022-03-27-15-41-14-98_a2db1b9502c98f2.jpg",
						bgcolor: ' #f0d9f0;'
					},
				],
				choice3_rightimgs: [
					"/static/picture/儿童花艺4_看图王.web.jpg",
					"/static/picture/儿童花艺5_看图王.web.jpg",
				], */
				tabnumber: 0,
			};
		},
		methods: {
			choose(index) {
				this.tabnumber = index;
				console.log(this.tabnumber)
			},
			developing() {
				this.$refs.uToast.show({
					title: '待开发中',
					type: 'warning',
					// url: '/pages/text/text'
				})
			},
			gotodetails(num) {
				console.log(num);
				uni.navigateTo({
					url:'/pages/details/details'
				})
			},
		}
	}
</script>

<style lang="scss">
	.choice3_tabs {
		padding-top: 210rpx;
		background-color: #ffffff;
		height: 270rpx;
		width: 750rpx;
		border-radius: 0rpx 0rpx 30rpx 30rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		//background-color: #007AFF;

		.choice3_tabs_word {
			text-align: center;

			text {
				color: #666666;
				font-size: 20rpx;
				line-height: 30rpx;
				word-spacing: 10rpx;
			}
		}
	}

	.tabs_more {
		width: 60rpx;
		height: 60rpx;
		margin-left: 700rpx;
		margin-top: -60rpx;
		display: flex;
		flex-direction: column;
		padding: 10rpx 0rpx;
		z-index: 500;

		.u-icon {
			top: 0rpx;
		}

		// background-image:linear-gradient(to right,#ffffff,#000000);
	}

	.choice3_scroll {
		height: 1064rpx;//882
		width: 750rpx;
		margin-top: 0rpx;

		.scroll {
			width: 335rpx;
			display: inline-block;
			vertical-align: top;
			margin-left: 30rpx;

			.images {
				margin-top: 20rpx;
				width: 375rpx;

				image {
					width: 335rpx;
				}
			}

		}

		/* 	.left_scroll {
			width: 375rpx;
			padding: 30rpx;
			background-color: #007AFF;

			.left_image {
				padding: 20rpx;
				width: 335rpx;
				height: 475rpx;
				background-color: #18B566;

				image {
					width: 300rpx;
					border-radius: 25rpx;
				}
			}
		}

		.right_scroll {
			width: 375rpx;

			.right_image {
				width: 335rpx;
				height: 475rpx;

				image {
					width: 300rpx;
					border-radius: 25rpx;
				}
			}
		} */

	}
</style>
