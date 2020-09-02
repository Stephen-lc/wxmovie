<template>
	<view class="container">
		<view class="search">
			<input type="text" @tap="search" placeholder="搜索" />
		</view>
		<view class="content">
			<view v-for="(items,index) in contentlist" :key="index">
				<view class="hit">
					<view class="hit_top">
						<text>{{items.name}}</text>
						<text @tap="tapList(items)">查看更多 ></text>
					</view>
					<scroll-view class="hit_main" scroll-x>
						<view class="main_view" v-for="item in items.list" :key="item">
							<view class="img_view">
								<image @tap="img_tap(item)" :src="item.images.large"></image>
							</view>
							<text class="text_title">{{item.title}}</text>
							<!-- 需要在 script 中绑定 value 变量 -->
							<view class="text_view">
								<uni-rate size="12" v-model="item.rating.average/2" />
								<text style="font-size: 12px;">{{item.rating.average}}</text>
							</view>
						</view>
					</scroll-view>
				</view>
			</view>




		</view>
	</view>
</template>

<script>
	import {
		uniRate
	} from '@dcloudio/uni-ui'
	export default {
		components: {
			uniRate
		},
		data() {
			return {
				contentlist: [{
						id: 0,
						name: "影院热映",
						list: [],
						url: "http://t.yushu.im/v2/movie/in_theaters",
						starts: 1,
						counts: 10,
					},
					{
						id: 1,
						name: "豆瓣热门",
						list: [],
						url: "http://t.yushu.im/v2/movie/top250",
						starts: 1,
						counts: 10
					},
					{
						id: 2,
						name: "近期热门剧集",
						list: [],
						url: "http://t.yushu.im/v2/movie/coming_soon",
						starts: 1,
						counts: 10
					},
					{
						id: 3,
						name: "电影本周口碑榜",
						list: [],
						url: "http://t.yushu.im/v2/movie/weekly",
						starts: 1,
						counts: 10
					},
					{
						id: 4,
						name: "北美票房榜",
						list: [],
						url: "http://t.yushu.im/v2/movie/us_box",
						starts: 1,
						counts: 10
					},
					{
						id: 5,
						name: "新片榜",
						list: [],
						url: "http://t.yushu.im/v2/movie/new_movies",
						starts: 1,
						counts: 10
					},
				],

				value: 4,
			}
		},
		onLoad() {
			for (let obj of this.contentlist) {
				this.req(obj.url, obj.starts, obj.counts, obj.id)
			}

		},
		methods: {
			search() {
				uni.navigateTo({
					url: "/pages/search/search"
				})
			},
			// 接口
			req(urls, starts, counts, arr) {
				uni.request({
					url: urls, //仅为示例，并非真实接口地址
					data: {
						apikey: '0df993c66c0c636e29ecbb5344252a4a',
						start: starts,
						count: counts
					},
					success: (res) => {
						// console.log(res)
						this.contentlist[arr].list = res.data.subjects;
					}
				});
			},
			// 详情按钮
			img_tap(obj) {
                 uni.navigateTo({
                 	url:"../filmdetails/filmdetails?id="+obj.id
                 })
			},
			
			tapList(obj){
				uni.navigateTo({
					url:"/pages/viewmore/viewmore?id="+obj.id +"&name="+obj.name +"&url="+obj.url
				})
			},
		}
	}
</script>

<style lang="less" scoped>
	.search {
		background-color: #1296db;
		padding: 15rpx 15rpx;

		input {
			width: 710rpx;
			border: 1px solid #ccc;
			border-radius: 5px;
			text-align: center;
			background-color: #fff;
			padding: 5rpx 5rpx;
		}
	}

	.content {
		padding-top: 10px;

		>view:not(:first-child) {
			margin-top: 20px;
		}

		>view {

			.hit_top {
				display: flex;
				padding: 0 10px;
				justify-content: space-between;
				align-items: center;

				text:nth-child(2) {
					color: #1296db;
				}
			}

			.hit_main {
				width: 100%;
				overflow: hidden;
				white-space: nowrap;
				padding: 10px 0;

				.main_view {
					margin: 0 10px;
					display: inline-block;

					.img_view {
						width: 100px;
						height: 150px;
						border-radius: 5px;

						image {
							width: 100px;
							height: 150px;
							border-radius: 5px;
						}
					}

					.text_title {
						display: inline-block;
						width: 100px;
						font-size: 14px;
						margin-top: 5px;
						overflow: hidden;
						text-overflow: ellipsis;
						white-space: nowrap;
					}

					.text_view {
						display: flex;
						justify-content: space-between;
						align-items: center;
					}
				}
			}
		}
	}
</style>
