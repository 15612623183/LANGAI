<template>
	<view>
		<button @click="gotosearch" type="warn">搜索</button>
		marketpage
	</view>
</template>

<script>
	export default {
		name:"marketpage",
		data() {
			return {
				
			};
		},
		methods:{
			gotosearch(){
				uni.navigateTo({
					url:'/pages/search/search'
				})
			}
		}
	}
</script>

<style>

</style>
