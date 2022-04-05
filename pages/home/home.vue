<template>
	<view>
		<view v-if="this.current === 0" class="">
			<homepage></homepage>
		</view>
		<view v-if="this.current === 1" class="">
			<marketpage></marketpage>
		</view>
		<view v-if="this.current === 3" class="">
			<identifypage></identifypage>
		</view>
		<view v-if="this.current === 4" class="">
			<mypage></mypage>
		</view>
		<view>
			<hans-tabber 
			:list="list" 
			style="position:fixed;bottom:0;width:100%;left:0;right:0;" 
			@tabChange="tabChange">
			</hans-tabber>
		</view>
	</view>
</template>

<script>
	import mypage from '@/components/mypage.vue'
	import marketpage from '@/components/marketpage.vue'
	import identifypage from '@/components/identifypage.vue'
	import homepage from '@/components/homepage.vue'
	import hansTabber from '@/components/hans-tabbar/hans-tabbar.vue'
	import {list} from '@/common/tabbar.js'
	export default {
		data() {
			return {
				current: 0,
				list: list,
				imagepath:[],
			}
		},
		methods: {
			handleSelectImage(){
				uni.chooseImage({
					count: 1, //图片数
					sourceType: ['camera'],
					success: res => {
						this.imagepath = res.tempFilePaths
					}
				})
			},
			tabChange(index) {
				if(index===2){
					this.handleSelectImage()
				}
				if(index!=2)
				{this.current = index}
				console.log("current=" + this.current)
			}
		},
		components: {
			hansTabber,
			homepage,
			mypage,
			marketpage,
			identifypage,
		},
		onLoad() {
			this.list
		}
	}
</script>

<style lang='scss'>
	.photography{
		width: 750rpx;
		height: 142rpx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		image{
			height: 100%;
		}
	}
</style>
