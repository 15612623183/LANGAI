<template>
	<view style="background-color: ;" class="">
		<view class="bg-ground">
			<image src="../../static/picture/下波浪.png" mode="widthFix"></image>
		</view>
		<view class="photography" >
			<image src="/static/icon/拍照按钮.png" mode="heightFix" @click="tabChange(2)"></image>
		</view>
		<view class="weui-tabbar" :class="extClass">
			<!-- 选中的时候往weui-tabbar__item加class:weui-bar__item_on -->
			<view @click="tabChange(index)" v-for="(item, index) in list" :key="index" class="weui-tabbar__item"
				:class="{'weui-bar__item_on':index === current}">
				<view class="" style="padding: 0rpx;;">
					
				
				<view style="position: relative;display:inline-block;">
					<image v-if="current === index" style="width: 80rpx;height: 80rpx;" :src="current === index ? item.selectedIconPath : item.iconPath" class="weui-tabbar__icon">
					</image>
					<image v-else style="width: 60rpx;height: 60rpx;" :src="current === index ? item.selectedIconPath : item.iconPath" class="weui-tabbar__icon">
					</image>
				</view>
				<!-- <view class="weui-tabbar__label" v-if="index === current" style="color: #000000;font-weight: 600;">{{ item.text }}</view> -->
				<view class="weui-tabbar__label" >{{ item.text }}</view>
				
				</view>
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		props: {
			list: {
				type: Array,
				default: function() {
					return []
				}
			}
		},
		data() {
			return {
				extClass: '',
				current: 0,
				imagepath: [],
			};
		},
		onShow(){
			uni.hideTabBar({
				animation:false
			})
		},
		methods: {
			tabChange(index) {
				if (index === this.current) {
					this.current=this.current;
				}
				else{
					this.current = index;
				}
				this.$emit('tabChange', index)
				console.log(index)
			},
			enable_camera() {
				console.log('enable camera success')
				
			}
		}
	};
</script>

<style lang="scss" scoped>
	.photography{
		z-index:999;
		width: 750rpx;
		height: 142rpx;
		margin-top: -185rpx;
		margin-bottom: 40rpx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		image{
			height: 100%;
		}
	}
	.weui-tabbar {
		border-radius: 60rpx 60rpx 0rpx 0rpx;
		display: flex;
		// position: relative;
		position: fixed;
		bottom: 0rpx;
		width: 100%;
		z-index: 500;
		// background-color: #ffffff;
	}

	// .weui-tabbar:before {
	// 	content: ' ';
	// 	position: absolute;
	// 	left: 0;
	// 	top: 0;
	// 	right: 0;
	// 	height: 1px;
	// 	border-top: 1rpx solid rgba(0, 0, 0, 0.1);
	// 	color: rgba(0, 0, 0, 0.1);
	// }
	.bg-ground {
		height: 140rpx;
		border-radius: 30rpx 30rpx 0rpx 0rpx;
		background-color: #ffffff;
		margin-bottom: 0rpx;
		display: flex;
		flex-direction: column;

		image {
			width: 100%;
			height: 100%;
			margin-top: 20rpx;
		}
	}

	.weui-tabbar__item {
		display: block;
		flex: 1;
		padding: 8px 0 4px;
		padding-bottom: calc(8px + constant(safe-area-inset-bottom));
		padding-bottom: calc(8px + env(safe-area-inset-bottom));
		font-size: 0;
		color: rgba(0, 0, 0, 0.5);
		text-align: center;
		-webkit-tap-highlight-color: rgba(0, 0, 0, 0);
	}

	.weui-tabbar__item:first-child {
		padding-left: constant(safe-area-inset-left);
		padding-left: env(safe-area-inset-left);
	}

	.weui-tabbar__item:last-child {
		padding-right: constant(safe-area-inset-right);
		padding-right: env(safe-area-inset-right);
	}

	.weui-tabbar__item.weui-bar__item_on .weui-tabbar__icon,
	{
		margin-top: -20rpx;
	}
	.weui-tabbar__item.weui-bar__item_on .weui-tabbar__icon>i,
	.weui-tabbar__item.weui-bar__item_on .weui-tabbar__label {
		color: #000000;
		font-weight: 600;
		
	}

	.weui-tabbar__icon {
		display: inline-block;
		width: 28px;
		height: 28px;
		margin-bottom: 2px;
	}

	i.weui-tabbar__icon,
	.weui-tabbar__icon>i {
		font-size: 24px;
		color: rgba(0, 0, 0, 0.5);
	}

	.weui-tabbar__icon image {
		width: 100%;
		height: 100%;
	}

	.weui-tabbar__label {
		color: #bfbfbf;
		font-size: 10px;
		line-height: 1.4;
	}
</style>
