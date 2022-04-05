<template>
	<view class="container">
		<view>
			<u-tabs-swiper ref="uTabs" bg-color='#f5f5f5' :show-bar='false' active-color='#f8cf51' :list="tabs"
				:current="current" @change="tabsChange" :is-scroll="false"></u-tabs-swiper>
		</view>
		<view class="line">
		</view>
		<swiper :current="swiperCurrent" @transition="transition" @animationfinish="animationfinish">
			<swiper-item class="swiper-item" v-for="(item, index) in tabs" :key="index">
				<scroll-view scroll-y style="height: 800rpx;width: 100%;" @scrolltolower="onreachBottom">
					<view v-for='(item,index) in flavorlist'>
						<view class="shihuablock">
							<view class="date">
								<text style="font-size:32rpx">{{item.day}}\n</text>
								<text style="font-size:24rpx">{{item.month}}</text>
							</view>
							<view class="dateline">
								<image src="/static/icon/dateline.png"></image>
							</view>
							<view class="flavoritem">
							<view class="flavorbox">
								<image @click="priview(item.src)" :src='item.src'></image>
								<text>{{item.value}}</text>
							</view>
							</view>
						</view>
						</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		name: "subsection",
		data() {
			return {
				imagesrc: 'https://bpic.51yuansu.com/pic3/cover/01/85/80/597034e2b47e3_610.jpg',
				save:[],
				flavorlist: [
					{
					day:3,
					month:"四月",
					value:"一二三四五，六七八九十。",
					src:"https://cdn.pixabay.com/photo/2014/04/14/20/11/pink-324175__340.jpg",
					},
					{
					day:2,
					month:"四月",
					value:"一二三四五，六七八九十。",
					src:"https://cdn.pixabay.com/photo/2012/03/01/00/55/garden-19830__340.jpg",
					},
					{
					day:1,
					month:"四月",
					value:"一二三四五，六七八九十。",
					src:"https://cdn.pixabay.com/photo/2013/07/21/13/00/rose-165819__340.jpg",
					},
				],
				tabs: [{
					name: '识花'
				}, {
					name: '日记'
				}, {
					name: '收藏'
				}, {
					name: '足迹'
				}],
				// 因为内部的滑动机制限制，请将tabs组件和swiper组件的current用不同变量赋值
				current: 0, // tabs组件的current值，表示当前活动的tab选项
				swiperCurrent: 0, // swiper组件的current值，表示当前那个swiper-item是活动的
			};
		},
		watch: {
			//监听Tabs的变化，一旦变化重新请求数据
			swiperCurrent() {
				console.log(this.swiperCurrent)
				this.getflavorlist()
			}
		},
		methods: {
			//图片预览
			priview(current){
				const urls = this.flavorlist.map(item=>{
					return item.src
					})
				uni.previewImage({
					current,
					urls
				})
			},
			//延时加载
			getflavorlist() {
				this.save=this.flavorlist
				this.flavorlist = []
				uni.showLoading()
				setTimeout(() => {
					this.flavorlist = this.save
					uni.hideLoading()
				}, 1000)
			},
			// tabs通知swiper切换
			tabsChange(index) {
				this.swiperCurrent = index;
			},
			// swiper-item左右移动，通知tabs的滑块跟随移动
			transition(e) {
				let dx = e.detail.dx;
				this.$refs.uTabs.setDx(dx);
			},
			// 由于swiper的内部机制问题，快速切换swiper不会触发dx的连续变化，需要在结束时重置状态
			// swiper滑动结束，分别设置tabs和swiper的状态
			animationfinish(e) {
				let current = e.detail.current;
				this.$refs.uTabs.setFinishCurrent(current);
				this.swiperCurrent = current;
				this.current = current;
			},
			// scroll-view到底部加载更多
			onreachBottom() {

			}
		}
	};
</script>

<style lang="scss">
	.container {
		swiper {
			height: 760rpx;
			display: flex
		}
	.shihuablock{
		background-color: #f5f5f5;
		display: flex;//块内容器felx放置
		flex-direction: row;//排列方式：行
		.date{
			width:70rpx;
			color: #116530;
			text-align: right;//文本对齐方式
		}
		.dateline{
			width:45rpx;
			image {
				margin-top: 30rpx;
				width: 40rpx;
				height: 500rpx;
			//border-radius: 25rpx; //图片圆角
			}
			
		}
		.flavoritem {
			width: 610rpx;
			height: 490rpx;
			padding: 25rpx; //内边框距离
			background-color: #e8e8cc;
			margin-top: 40rpx;//外边框距离
			align-items: center;
			.flavorbox{
				width: 555rpx;
				height: 440rpx;
				image {
				width: 555rpx;
				height: 400rpx;
				//border-radius: 25rpx; //图片圆角
				}
			}	
		}
	}
		.line {
			width: 750rpx;
			height: 10rpx;
			background-image: linear-gradient(to bottom, #feecb7, #f5f5f5);//颜色渐变（从上到下，从color1到color2）
		}
	}
</style>
