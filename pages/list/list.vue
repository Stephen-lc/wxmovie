<template>
	<view class="container">
		<view class="top">
			<image src="../../static/movie_hot.png" mode=""></image>
			<image src="../../static/movie_hot2.png" mode=""></image>
		</view>

		<view class="center">
			<view class="center_left" v-for="(item,index) in list" :key="index">
				
				<view class="left_img" @tap="img_tap(item)">
					<image style="width: 100px;height: 100px;" :src="item.url" mode=""></image>
				</view>
				
				<view class="center_right">
					<view class="right_content">
						<view class="data_view" v-for="(data,index) in item.arr" :key="index">
						    <text>{{data.sub}}.</text>
							<text>{{data.title}}</text>
							<text>{{data.rating.average}}</text>
						</view>
					</view>
				</view>
				
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
						id: 0,
						url: "https://img1.doubanio.com/img/files/file-1543460329.png",
						src: "http://t.yushu.im/v2/movie/top250?apikey=0df993c66c0c636e29ecbb5344252a4a&start=20&count=1",
						start: 1,
						counts: 3,
						name:"Top250",
						arr: []
					},
					{
						id: 1,
						url: "https://img1.doubanio.com/img/files/file-1543460329.png",
						src: "http://t.yushu.im/v2/movie/in_theaters?apikey=0df993c66c0c636e29ecbb5344252a4a&start=0&count=10",
						start: 1,
						name:"最近热映",
						counts: 3,
						arr: []
					},
					{
						id: 2,
						url: "https://img1.doubanio.com/img/files/file-1543460329.png",
						src: "http://t.yushu.im/v2/movie/coming_soon?apikey=0df993c66c0c636e29ecbb5344252a4a",
						start: 1,
						counts: 3,
						name:"即将上映",
						arr: []
					},
				]
			}
		},
		onLoad() {
			for (let obj of this.list) {
				this.req(obj.src, obj.start, obj.counts, obj.id)
			}
		},
		methods: {
			// 榜单详情
			img_tap(obj) {
				uni.navigateTo({
					url: "/pages/listdetails/listdetails?id=" + obj.id + "&url=" + obj.url + "&src=" + obj.src+"$name="+obj.name
				})
			},

			// 接口
			req(urls, starts, counts, num) {
				uni.request({
					url: urls, //仅为示例，并非真实接口地址
					data: {
						apikey: '0df993c66c0c636e29ecbb5344252a4a',
						start: starts,
						count: counts
					},
					success: (res) => {

						let sub=1
						for(let obj of res.data.subjects){
							obj.sub=sub++
						}
						this.list[num].arr = res.data.subjects;
						
					}
				});
			},

		}
	}
</script>

<style lang="less" scoped>
	.top {
		width: 100%;
		background-color: #fff;
		padding: 20px 20px 0 20px;
		image{
			width: 680rpx;
			height: 200px;
			margin-bottom: 10px;
			border-radius: 10px;
		}
	}

	.center {
		padding: 0px 20px;

		>.center_left {
			padding: 10px 0;
			display: flex;
			justify-content: space-between;

			.left_img {
				width: 100px;
				height: 100px;
				background-color: #343038;
				border-radius: 5px;
			}

			.center_right {
				flex: 1;
				margin-left: 5px;
				padding: 10px 0;

				.right_content {
					// border: 1px solid #ccc;
					border-left: none;

					.data_view {
						display: flex;
						justify-content: flex-start;
						align-items: center;
						padding-left: 20px;
						text:nth-child(2){
							display: inline-block;
							width: 200rpx;
							font-size: 14px;
							line-height: 28px;
							margin: 0 5px;
							overflow: hidden;
							text-overflow: ellipsis;
							white-space: nowrap;
						}
					}
				}
			}
		}
	}
</style>
