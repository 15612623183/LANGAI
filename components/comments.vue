<template>
	<view class="">
		<view v-show="datainit()" style="margin-top: 500rpx;">
		</view>
		<view style="margin-top: 50rpx;">
			待添加
		</view>
		<view class="" style="margin-left: 30rpx;">
			<view class="comment-num">
				<view> {{commentData.commentSize}} 评论</view>
			</view>
			<view class="comment-box" v-for="(item,index) in commentData.comment" :key="index">
				<view class="comment-box-item">
					<view>
						<image :src="item.avatarUrl || emptyAvatar" mode="aspectFill" class="avatar"></image>
					</view>
					<view class="comment-main">
						<!-- 父评论体-start -->
						<view class="comment-main-top">
							<!-- 评论者昵称-start -->
							<view class="nick-name-box">
								<view class="nick-name">{{item.nickName}}</view>
							</view>
							<!-- 评论者昵称-end -->
							<!-- 点赞按钮-start -->
							<view class="zan-box" style="display: flex;" @click="like(item.id)">
								<text
									:class="item.hasLike ? 'isLike' : 'notLike'">{{item.likeNum == 0 ? '' : item.likeNum}}</text>
								<view v-if="item.hasLike">
									<u-icon size="14rpx" name="heart-fill" color="#dd5050"></u-icon>
								</view>
								<view v-else>
									<u-icon size="14rpx" name="heart"></u-icon>
								</view>
							</view>
							<!-- 点赞按钮-end -->
						</view>
						<view class="comment-main-content">
							{{item.content.length > 60 ? item.content.slice(0, 59) : item.content}}
							<!-- <text v-if="item.content.length > 60">
						{{item.hasShowMore ? item.content.slice(59) : '...'}}
						<text class="foot-btn" @click="showMore(item.id)">
							{{item.hasShowMore ? '收起' : '展开'}}
						</text>
					</text> -->
						</view>
						<view class="comment-main-foot">
							<view class="foot-time">{{item.createTime}}</view>
							<view class="foot-btn" @click="reply(item.nickName,item.nickName,item.id)">回复</view>
							<view class="foot-btn" v-if="item.owner" @click="confirmDelete(item.id)">删除</view>
						</view>
						<!-- 父评论体-end -->
						<!-- 子评论列表-start -->
						<view v-if="item.children" class="comment-sub-box">
							<view class="comment-sub-item" v-for="each in item.children">
								<view>
									<image :src="each.avatarUrl || emptyAvatar" mode="aspectFill" class="child_avatar">
									</image>
								</view>
								<view class="comment-main">
									<view class="sub-comment-main-top">
										<view class="nick-name">
											<text>{{each.nickName}}</text>
											<view class=""
												style="margin-left: 10rpx;display: flex;border-radius: 15rpx;width: 60rpx;height: 30rpx;background-color: #e7e7e7;align-items: center;">
												<text v-if="each.nickName"
													style="font-size: 24rpx;color: #666666;margin-left: 6rpx;">作者</text>
											</view>
										</view>
										<!-- 点赞按钮-start -->
										<view class="zan-box" style="display: flex;" @click="like(each.id)">
											<text
												:class="each.hasLike ? 'isLike' : 'notLike'">{{each.likeNum == 0 ? '抢首赞' : each.likeNum}}</text>
											<view v-if="!each.hasLike">
												<u-icon size="14rpx" name="heart-fill" color="#dd5050"></u-icon>
											</view>
											<view v-else>
												<u-icon size="14rpx" name="heart"></u-icon>
											</view>
										</view>
										<!-- 点赞按钮-end -->
									</view>
									<view class="comment-main-content">
										{{each.content.length > 60 ? each.content.slice(0, 59) : each.content}}
										<!-- 	<span v-if="each.content.length > 60">
									{{each.hasShowMore ? each.content.slice(59) : '...'}}
									<span class="foot-btn" @click="showMore(each.id)">
										{{each.hasShowMore ? '收起' : '展开'}}
									</span>
								</span> -->
									</view>
									<view class="comment-main-foot">
										<view class="foot-time">{{each.createTime}}</view>
										<view class="foot-btn" @click="reply(item.nickName,each.nickName,item.id)">
											回复</view>
										<view class="foot-btn" v-if="each.owner" @click="confirmDelete(each.id)">删除
										</view>
									</view>
								</view>
							</view>
						</view>
					</view>
					<!-- 子评论列表-end -->
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		name: 'comments',
		data() {
			return {
				commentData: [],
				readNumer: 193,
				commentList: [{
						"id": 1, // 唯一主键
						"owner": false, // 是否是拥有者，为true则可以删除，管理员全部为true
						"hasLike": false, // 是否点赞
						"likeNum": 182, // 点赞数量
						"avatarUrl": "https://inews.gtimg.com/newsapp_ls/0/13797755537/0", // 评论者头像地址
						"nickName": "KKK", // 评论者昵称，昵称过长请在后端截断
						"content": "蹲个教程！太好看了！", // 评论内容
						"parentId": null, // 所属评论的唯一主键
						"createTime": "7小时前" // 创建时间
					},
					{
						"id": 2,
						"owner": false,
						"hasLike": false,
						"likeNum": 13,
						"avatarUrl": "https://inews.gtimg.com/newsapp_ls/0/13797761970/0",
						"nickName": "胖胖猫",
						"content": "问一下黏土下面要插画泥吗",
						"parentId": null,
						"createTime": "2月26日"
					},
					{
						"id": 3,
						"owner": true,
						"hasLike": true,
						"likeNum": 1,
						"avatarUrl": "https://inews.gtimg.com/newsapp_ls/0/13797763270/0",
						"nickName": "花园宝妈",
						"content": "可加可不加",
						"parentId": 2,
						"createTime": "2月26日"
					},
					{
						"id": 4,
						"owner": false,
						"hasLike": false,
						"likeNum": 0,
						"avatarUrl": "https://inews.gtimg.com/newsapp_ls/0/13797755537/0",
						"nickName": "小雏菊",
						"content": "简直绝美啊~",
						"parentId": null,
						"createTime": "1月15日"
					},
					{
						"id": 5,
						"owner": true,
						"hasLike": false,
						"likeNum": 0,
						"avatarUrl": "https://inews.gtimg.com/newsapp_ls/0/13797755537/0",
						"nickName": "花园宝妈",
						"content": "蟹蟹~",
						"parentId": 4,
						"createTime": "1月15日"
					}
				]
			}
		},
		methods: {
			//将后端返回的信息进行整理
			getTree(data) {
				let result = [];
				let map = {};
				data.forEach(item => {
					map[item.id] = item;
				});
				data.forEach(item => {
					let parent = map[item.parentId];
					if (parent) {
						(parent.children || (parent.children = [])).push(item);
					} else {
						result.push(item);
					}
				});
				return result;
			},
			datainit() {
				this.commentData = {
					"readNumer": this.readNumer,
					"commentSize": this.commentList.length,
					"comment": this.getTree(this.commentList)
				}
				console.log(this.commentData)
			},
			reply(pUser, reUser, pId) {
				this.pUser = pUser;
				this.commentReq.pId = pId;
				if (reUser) {
					this.commentReq.content = '@' + reUser + ' ';
				} else {
					this.commentReq.content = '';
				}
				this.showTag = true;
				this.commentInput();
			},

		},

	}
</script>

<style lang="scss">
	.comment-box {
		padding: 10rpx 0;
		border-bottom-style: solid;
		border-bottom-width: 1rpx;
		border-bottom-color: #dddcdc;
	}

	.comment-box-item {
		display: flex;
	}

	.avatar {
		width: 70rpx;
		height: 70rpx;
		border-radius: 50%;
	}

	.child_avatar {
		width: 40rpx;
		height: 40rpx;
		border-radius: 50%;
	}

	.comment-main {
		padding-left: 20rpx;
	}

	.comment-main-top {
		width: 600rpx;
		padding-top: 6rpx;
		display: flex;
		justify-content: space-between;
	}

	.nick-name-box {
		display: flex;
		align-items: center;
	}

	.nick-name {
		color: #999999;
		display: flex;
		align-items: center;
	}

	.isLike {
		font-size: 28rpx;
		padding-right: 10rpx;
		color: #2d8cf0;
	}

	.notLike {
		font-size: 28rpx;
		padding-right: 10rpx;
		color: #999999;
	}

	.comment-main-content {
		padding: 10rpx 10rpx 10rpx 0;
	}

	.comment-main-foot {
		display: flex;
		font-size: 22rpx;
		padding-bottom: 20rpx;
	}

	.foot-btn {
		padding-left: 10rpx;
		color: #007AFF;
	}


	.comment-sub-box {
		//padding-bottom: 20rpx;
	}

	.comment-sub-item {
		display: flex;
	}

	.sub-comment-main-top {
		width: 540rpx;
		padding-top: 6rpx;
		display: flex;
		justify-content: space-between;
	}
</style>
