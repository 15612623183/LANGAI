<template>
	<view class="result_bar_block">
		<view class="result_bar">
			<view @click="result_choose(index)" v-if="" class="classification_choice"
				v-for="(item,index) in result_classification" :key="index">
				<view style="display: flex;flex-direction: column;align-items: center;">
					<view :class="(selectionnum === index) ? 'word_active' : 'word'">
						<text>{{item}}</text>
					</view>
					<image v-if="selectionnum === index" :src="bottom_selection_icon" mode="widthFix"
						style="width: 40rpx;">
					</image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'result-bar',
		data() {
			return {
				result_classification: [
					"笔记",
					"用户",
				],
				bottom_selection_icon: '/static/icon/选择下标.png',
				selectionnum: 0,
			}
		},
		methods: {
			result_choose(index) {
				this.selectionnum = index;
				console.log("可爱花束"+this.selectionnum);
				this.$emit('result_choose',this.selectionnum)
			},
		},
	}
</script>

<style lang="scss">
	.word_active {
		display: flex;

		text {
			font-size: 25rpx;
			color: #000000;
		}
	}

	.word {
		display: flex;

		text {
			font-size: 25rpx;
			color: #999999;
		}
	}

	.result_bar_block {
		width: 750rpx;
		height: 55rpx;
		margin-top: 10rpx;
		border-bottom: #dcdcdc solid 1rpx;

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
	}
</style>
