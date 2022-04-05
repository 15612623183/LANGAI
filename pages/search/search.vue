<template>
	<view>
		<view class="search_head">
			<!-- 搜索框-start -->
			<view class="searchblock">
				<view class="back_icon">
					<u-icon class="uicon" name="/static/icon/back.png" size="18rpx" @click="goback"></u-icon>
				</view>
				<view class="inputblock">
					<image src="/static/icon/搜索.png" mode="widthFix" style="width: 40rpx;margin-left: 20rpx;"></image>
					<input type="text" search-icon='/static/icon/search.png'
						style="width: 420rpx;margin-left: 20rpx;font-size: 25rpx;" placeholder="可爱花束"
						@input="inputChange" @search="doSearch(false)" @confirm="doSearch(false)" v-model="keyword">
					</input>
					<!-- 输入框 :placeholder：未输入时显示内容，v-model：绑定字段，maxlength：设置输入长度，@input：输入框内容有变化时触发事件 @confirm：能让手机输入框的确认变成搜索-->
					<image src="/static/icon/X.png" mode="widthFix" style="margin-right: 30rpx;width: 21rpx;"
						v-if="isDelShow" @click="clear"></image>
				</view>
				<view>
					<view style="margin-left: 30rpx;color: #999999;" @tap="doSearch(false)">搜索</view><!-- 执行搜索事件 -->
				</view>
			</view>
			<!-- 搜索框-end -->
			<resultbar @result_choose='result_choose' v-if="showresult"></resultbar>
			<resultnotes v-if="showresult & selectionnum === 0"></resultnotes>
			<resultuser v-if="showresult & selectionnum === 1"></resultuser>
		</view>
		
		<view class="" style="padding-top: 150rpx;">
			
		<!-- 打开下拉搜索栏 -->
		<view v-if="openlist & !showresult" class="list">
			<view @click="findchooseitem(index)" class="filterList" v-for="(item,index) in filterList" :key="index">
				<view class="" v-if="chooselist[index] === '可爱花束'" style="display: flex;align-items: center;justify-content: space-between;">
					<rich-text  style="font-size: 30rpx;color: #999999;" :nodes="item"></rich-text>
					<text style="font-size: 22rpx;color: #999999;">46k+ 笔记</text>
				</view>
				<rich-text v-else style="font-size: 30rpx;color: #999999;" :nodes="item"></rich-text>
			</view>
		</view>
		<!-- 关闭下拉搜索栏，展示搜索帮助 -->
		<view v-if="!openlist & !showresult" class="">
			<!-- 历史记录 -->
			<view class="record">
				<view class="record_heand">
					<text style="font-size: 25rpx;margin-top: 10rpx;">历史记录</text>
					<image src="/static/icon/垃圾桶.png" mode="widthFix" @click="delete_key"></image><!-- 点击历史记录直接执行搜索 -->
				</view>
				<!-- 搜索历史内容 -->
				<scroll-view class="keyword-box" v-show="!isShowKeywordList" scroll-y>
					<view class="keyword-block" v-if="oldKeywordList.length>0">
						<!-- v-if:判断是否存在历史记录 -->
						<view class="keyword">
							<view style="border-color: #ffca31;" v-for="(keyword,index) in oldKeywordList"
								@tap="doSearch(keyword)" :key="index">
								<text style="font-size: 26rpx;">{{keyword}}</text>
							</view><!-- 循环渲染历史记录数组内容 -->
						</view>
					</view>
				</scroll-view>
			</view>
			<!-- 猜你喜欢 -->
			<view class="record">
				<view class="record_heand">
					<text style="font-size: 25rpx;">猜你喜欢</text>
					<image src="/static/icon/刷新.png" mode="widthFix" @tap="hotToggle"></image>
					<!-- ：class:判断是否点击，每次点击会改变绑定的字段(也可以是样式)，根据字段不同展示不同的图标	自定义图标在style	 -->
				</view>
				<!-- 猜你喜欢内容 -->
				<scroll-view class="keyword-box" v-show="!isShowKeywordList" scroll-y>
					<!-- 判断是否展示猜你喜欢 -->
					<view class="keyword-block" v-if="forbid==''">
						<view class="keyword">
							<view style="border-color: #65abd7;border-radius: ;"
								v-for="(keyword,index) in likekeywordList" @tap="doSearch(keyword)" :key="index">
								<text style="font-size: 26rpx;">{{keyword}}</text>
							</view><!-- 循环猜你喜欢标签，并添加点击标签搜索事件 -->
						</view>
					</view>
					<view class="yingcang" v-else>
						<view>当前猜你喜欢已隐藏</view>
					</view>
				</scroll-view>
			</view>
			<!-- 热门话题 -->
			<view class="record">
				<view class="record_heand">
					<text style="font-size: 25rpx;">热门话题</text>
				</view>
				<!-- 热门话题内容 -->
				<scroll-view class="keyword-box" scroll-y>
					<view class="keyword-block">
						<view class="hotkeyword">
							<view style="display: flex;align-items: center;padding-bottom: 40rpx;"
								v-for="(keyword,index) in hotkeywordList" @tap="doSearch(keyword.name)" :key="index">
								<view class="dot" :style="{'background-color':keyword.color}"></view>
								<text style="margin-left: 25rpx;font-size: 26rpx;">{{keyword.name}}</text>
							</view><!-- 循环热门话题标签，并添加点击标签搜索事件 -->
						</view>
					</view>
				</scroll-view>
			</view>
		</view>
		
		</view>

	</view>
</template>

<script>
	import resultbar from '@/components/search/result-bar.vue'
	import resultnotes from '@/components/search/result-notes.vue'
	import resultuser from '@/components/search/result-user.vue'
	export default {
		components: {
			resultbar,
			resultnotes,
			resultuser
		},
		props: {

			placeholder: { //占位符，为输入时显示的内容
				type: String,
				default: '娱乐，好玩的'
			},

		},
		data() {
			return {
				keyword: "朗爱APP",
				list: [
					'可爱花束',
					'可爱花束包装',
					'可爱风花束',
					'可爱玫瑰花束',
					'可爱小花束',
					'可爱小熊花束',
					'可爱黏土花束'
				],
				chooselist: [],
				filterList: [],
				openlist: false,
				showresult: false,
				keyword: "", //关键字
				oldKeywordList: [], //历史记录
				likekeywordList: [], //猜你喜欢
				hotkeywordList: [{
					name: '四叶草堂社区花园',
					color: '#dd5050'
				}, {
					name: '当龙猫遇上花花',
					color: '#ffca31'
				}, {
					name: '儿童节宠物花束',
					color: '#65abd7'
				}, {
					name: '鲜花味棒棒糖',
					color: '#999999'
				}, {
					name: '植物敲拓染',
					color: '#999999'
				}, {
					name: '千花手机壳',
					color: '#999999'
				}, {
					name: '蓝色小花婆婆纳',
					color: '#999999'
				}, ],



				isShowKeywordList: false,
				isDelShow: false, //判断是否出现删除标志
				forbid: "", //热搜显隐标志

				showsearchbtn: false,
				searchval: '',
				target: 0,
				selectionnum: 0,//搜索结果选择序号

			}
		},
		onLoad() {
			this.init();
		},
		methods: {
			result_choose(index){
				console.log('收到参数'+index);
				this.selectionnum = index;
			},
			//返回主页
			goback() {
				uni.navigateBack({
				})
			},
			//查找搜索项
			findchooseitem(index) {
				let _this = this
				console.log('点击了' + index)
				console.log(this.chooselist)
				_this.doSearch(this.chooselist[index])
				this.filterList = []
			},

			set(e) {
				console.log('调用了函数')
				let value = e.detail.value;
				if (!value) {
					this.filterList = this.list;
					return;
				}

				let filterArr = [];
				let chooseArr = [];
				// 过滤出符合条件的值
				this.list.forEach((item, index) => {
					if (item.includes(value)) {
						filterArr.push(this.join(item, value));
						chooseArr.push(this.list[index]);
						console.log('符合条件的序号：' + index)
					}
				});

				this.filterList = filterArr;
				this.chooselist = chooseArr;

				if (e.detail.value == 0) {
					this.filterList = []
				}

			},
			// 拼接
			join(str, key) {
				var reg = new RegExp((`(${key})`), "gm");
				var replace = '<span style="color:#000000;font-weight:bold;">$1</span>';
				return str.replace(reg, replace);
			},
			//页面刷新渲染
			init() {
				//this.loadDefaultKeyword();
				this.loadOldKeyword();
				this.loadlikekeyword();

			},
			//页面渲染时自动读取本地存储的历史记录
			loadOldKeyword() {
				uni.getStorage({
					key: 'OldKeys',
					success: (res) => {
						var OldKeys = JSON.parse(res.data);
						this.oldKeywordList = OldKeys;
					},
				})
			},
			//页面渲染加载热门搜索关键字，后期通过后台获取数据赋值
			loadlikekeyword() {
				this.likekeywordList = ['春日限定樱花海', '手工花篮编制', '水仙花种子', '可爱花朵蔬菜抱枕'];
			},
			//监听输入
			inputChange: async function(event) {
				let _this = this
				//判断输入框是否有值输入，决定是否出现删除符号
				if (this.keyword.length > 0) {
					console.log(this.keyword.length)
					this.isDelShow = true;
					this.openlist = true;
					console.log("搜索栏有输入")
				} else {
					this.isDelShow = false;
					this.openlist = false;
					console.log("搜索栏无输入")
				}
				//兼容引入组件时传入参数情况
				var keyword = event.detail ? event.detail.value : event;
				if (!keyword) {
					this.isShowKeywordList = false;
					return;
				}
				this.isShowKeywordList = true;
				this.showresult = false;
				//替换自己接口
				_this.set(event);
			},
			//执行搜索
			doSearch(keyword) {
				if (keyword == '') {
					if (this.keyword.length == 0) { //判断是否输入内容
						console.log("不执行搜索")
						uni.showToast({ //没有则弹出提示框，提示未输入
							title: "请输入关键字",
							icon: 'none',

						})
					} else if (this.keyword.length >= 1) { //若存在输入内容，执行搜索
						console.log("执行了搜索")
						keyword = keyword === false ? this.keyword : keyword;
						this.keyword = keyword;
						this.saveKeyword(keyword); //保存为历史,执行此事件
						uni.showToast({ //弹出提示框
							title: keyword,
							icon: 'none',
							duration: 2000
						});
						this.showresult = true;
						this.openlist = false;
					}
				} else if (keyword != '') {
					this.keyword = keyword
					console.log("执行了搜索")
					keyword = keyword === false ? this.keyword : keyword;
					this.keyword = keyword;
					this.saveKeyword(keyword); //保存为历史,执行此事件
					uni.showToast({
						title: keyword,
						icon: 'none',
						duration: 2000
					})
					this.showresult = true;
					this.openlist = false;
				}

			},
			//保存关键字到历史
			saveKeyword(keyword) {
				uni.getStorage({
					key: 'OldKeys',
					success: (res) => {
						var OldKeys = JSON.parse(res.data);
						var findIndex = OldKeys.indexOf(keyword);
						if (findIndex == -1) {
							OldKeys.unshift(keyword);
						} else {
							OldKeys.splice(findIndex, 1);
							OldKeys.unshift(keyword);
						}
						//最多五个记录
						OldKeys.length > 5 && OldKeys.pop(); //删除数组尾部元素
						uni.setStorage({
							key: 'OldKeys',
							data: JSON.stringify(OldKeys)
						});
						this.oldKeywordList = OldKeys; //更新历史记录
					},
					fail: (e) => {
						var OldKeys = [keyword];
						uni.setStorage({
							key: 'OldKeys',
							data: JSON.stringify(OldKeys)
						});
						this.oldKeywordList = OldKeys; //更新历史记录
					}
				})
			},
			//清空输入框
			clear() {
				console.log(this.keyword)
				uni.hideKeyboard();
				this.keyword = '';
				this.inputChange('')
				console.log("没有" + this.keyword.length + this.keyword)
			},
			//删除历史记录-全部
			delete_key() {
				uni.showModal({
					content: '确定清除历史搜索记录？',
					success: (res) => {
						if (res.confirm) {
							this.oldKeywordList = [];
							uni.removeStorage({
								key: 'OldKeys'
							});
						} else if (res.cancenl) {
							console.log("用户点击取消")
						}
					}
				})
			},
			//热门开关
			hotToggle() {
				this.forbid = this.forbid ? '' : '1' //两个图标的差别在这个数字"1"上
			},
		},
		onBackPress() {
			uni.redirectTo({
				url: '/pages/home/home'
			});
		},
	}
</script>

<style lang="scss">
	.search_head {
		width: 750rpx;
		position: fixed;
		z-index: 500;
		background-color: #f5f5f5;
		padding-top: 70rpx;
		border-bottom: #dcdcdc solid 1rpx;
	}

	.searchblock {
		padding-bottom: 20rpx;
		height: 80rpx;
		display: flex;
		flex-direction: row;
		align-items: center;

		.back_icon {
			width: 90rpx;
			height: 60rpx;

			.uicon {
				margin-left: 30rpx;
				margin-top: 15rpx;
			}
		}

		.inputblock {
			width: 540rpx;
			height: 60rpx;
			background-color: #ffe7a0;
			border-radius: 30rpx;
			display: flex;
			flex-direction: row;
			align-items: center;
		}
	}



	.u-action {
		background-color: #55ff00;
	}

	.searchclass {
		margin-top: 70rpx;
		height: 60rpx;
		display: flex;

		.back_icon {
			width: 90rpx;

			.uicon {
				margin-left: 30rpx;
				margin-top: 15rpx;
			}
		}
	}


	.list {
		height: 300rpx;

		.filterList {
			margin-left: 20rpx;
			padding: 30rpx 0rpx;
			width: 690rpx;

			&+view {
				width: 690;
				border-top: #e5e5e5 solid 1px;
			}
		}
	}

	.hotkeyword {
		width: 90%;
		padding: 0rpx 55rpx;
		display: flex;
		flex-direction: column;
		justify-content: space-around;

		.dot {
			width: 10rpx;
			height: 10rpx;
			border-radius: 5rpx;
		}
	}

	.record {
		
		.record_heand {
			margin-top: 20rpx;
			display: flex;
			align-items: center;

			text {
				width: 620rpx;
				height: 50rpx;
				margin-left: 35rpx;
			}

			image {
				width: 30rpx;
			}
		}

		.record_buttom {}
	}

	.keyword-box .keyword-block {
		padding: 10upx 0;
	}

	.keyword-box .keyword-block .keyword-list-header {
		width: 94%;
		padding: 10upx 3%;
		font-size: 27upx;
		color: #333;
		display: flex;
		justify-content: space-between;
	}

	.keyword-box .keyword-block .keyword-list-header image {
		width: 40upx;
		height: 40upx;
	}

	.keyword-box .keyword-block .keyword {
		width: 100%;
		padding: 0rpx 35rpx;
		display: flex;
		flex-flow: wrap;
		justify-content: flex-start;
	}

	.keyword-box .keyword-block .hide-hot-tis {
		display: flex;
		justify-content: center;
		font-size: 28upx;
		color: #6b6b6b;
	}

	.keyword-box .keyword-block .keyword>view {
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 60upx;
		border-style: solid; //实线边框
		padding: 0 20upx;
		margin: 10upx 20upx 10upx 0;
		height: 60upx;
		font-size: 28upx;
		background-color: #FFFFFF;
		color: #000000;
	}

	.yingcang {
		margin: 50rpx 50rpx;
	}
</style>
