<template>
	<view>
		<view>
			<view>
				拍照
			</view>
			<view class="drop">
				<view class="dropdown">
					<u-dropdown>
						<u-dropdown-item title="">
							<view calss="datastyle" style="background-color: #eec201;">
								<scroll-view scroll-y="true" style="height: 200rpx;">
									<view v-for="(item,index) in Data" class="u-text-center">{{item}}</view>
								</scroll-view>
							</view>
						</u-dropdown-item>
					</u-dropdown>
				</view>
			</view>
		</view>
		<u-tabbar v-model="current" :list="tabbar" :mid-button="true"></u-tabbar>
	</view>
</template>

<script>
	import {tabbar} from '../../common/tabbar.js'
	export default {
		data() {
			return {
				current:3,
				tabbar: tabbar,
				Data:["3.26","3.25","3.24","3.23","3.22","3.21"]
			}
		},
		methods: {
		},
		onShow() {
			uni.hideTabBar({
				animation: false
			})
		},
		onLoad() {
			this.tabbar
		}
	}
</script>

<style lang="scss">
	.drop {
		display: flex;
		flex-direction: row;
		justify-content: flex-end;
		width: 750rpx;
		.dropdown{
			width: 80rpx
			
		}
		.datastyle{
			height: 400rpx;
		}
	}
</style>
