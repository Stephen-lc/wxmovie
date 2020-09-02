<template>
	<view class="container">
		<view class="top">
			<view class="top_left">
				<image :src="list.images.large" mode=""></image>
			</view>
			<view class="top_right">
				<view>
					<text class="title_view">{{list.title}}</text>
					<text>{{list.title}}</text>
				</view>
				<view class="text_view">
					<text>{{list.genres}} / {{list.countries}} </text>
				</view>
				<view class="look_view">
					<view><image src="../../static/love.png" mode=""></image>想看</view>
					<view><image src="../../static/xx.png" mode=""></image>看过</view>
				</view>
			</view>
		</view>
		<view class="img">
			<image src="../../static/moive.png" mode=""></image>
		</view>
		<view class="center">
			<view class="title">
				简介
			</view>
			<text>{{list.summary}}</text>
		</view>
		
		<view class="foot">
			<text>影人</text>
			<view >
				<image v-for="item in list.casts" :key="item" :src="item.avatars.large"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
			}
		},
		onLoad(obj) {
			let id = obj.id
			uni.request({
				url: 'http://t.yushu.im/v2/movie/subject/' + id + '?apikey=0df993c66c0c636e29ecbb5344252a4a', //仅为示例，并非真实接口地址。
				success: (res) => {
					// console.log(res);
					this.list = res.data;
					console.log(this.list)
				}
			});

		},
		methods: {

		}
	}
</script>

<style lang="less" scoped>
	.container {
		padding: 20px;
		height: 100%;
		background-color: #F5F6F8;

		.top {
			padding: 10px 0;
			border: 1px solid #eee;
			display: flex;
			justify-content: space-between;



			.top_left {
				image {
					width: 100px;
					height: 150px;
					border-radius: 5px;
				}
			}

			.top_right {
				flex: 1;
				margin-left: 20px;

				>view:first-child {
					display: flex;
					flex-direction: column;
					.title_view {
						width: 100px;
						font-size: 14px;
						margin-top: 5px;
						overflow: hidden;
						text-overflow: ellipsis;
						white-space: nowrap;
						font-weight: bold;
						font-size: 20px;
					}

					>text {
						display: inline-block;
						width: 100px;
						font-size: 14px;
						margin-top: 5px;
						overflow: hidden;
						text-overflow: ellipsis;
						white-space: nowrap;
					}
				}

				.text_view {
					>text {
						font-size: 12px;
					}
				}

				.look_view {
					display: flex;
					justify-content: flex-start;
					align-items: center;
					margin-top: 20px;
                    
					>view {
						width: 100px;
						height: 30px;
						line-height: 30px;
						text-align: center;
						border-radius: 5px;
						background-color: #fff;
						display: flex;
						align-items: center;
						justify-content: center;
						image{
							width: 20px;
							height: 20px;
						}
					}

					>view:last-child {
						margin-left: 20px;
					}
				}
			}
		}

        .img{
			width: 680rpx;
			height: 150px;
			>image{
				width: 680rpx;
				height: 150px;
			}
		}
        .center{
			margin-top: 20px;
			.title{
				line-height: 28px;
			}
			>text{
				line-height: 24px;
			}
		}
		
		.foot{
			margin-top: 20px;
			
			>view{
				display: flex;
				justify-content: space-between;
				margin-top: 10px;
				>image{
					width: 100px;
					height:100px;
				}
			}
		}
	}
</style>
