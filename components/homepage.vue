<template>
	<view style="background-color: #f5f5f5;height: 1334rpx;">
		<homehead @choose="choose">
		</homehead>
		<view class="" v-if="this.choice === 0">
			<homebody1></homebody1>
		</view>
		<view class="" v-if="this.choice === 1">
			<homebody2></homebody2>
		</view>
		<view class="" v-if="this.choice === 2">
			<homebody3></homebody3>
		</view>

	</view>
</template>

<script>
	import homehead from '@/components/home/home-head.vue'
	import homebody1 from '@/components/home/home-body1.vue'
	import homebody2 from '@/components/home/home-body2.vue'
	import homebody3 from '@/components/home/home-body3.vue'
	export default {
		name: "homepage",
		data() {
			return {
				choice: 1,
			};
		},
		components: {
			homehead,
			homebody1,
			homebody2,
			homebody3,
		},
		methods: {
			choose(index) {
				console.log(this.choice)
				this.choice = index;
			},
		}

	}
</script>

<style>

</style>
