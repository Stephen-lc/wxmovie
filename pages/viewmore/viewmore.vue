<template>
	<view class="container">
		<view class="main">
			<view class="title">即将上映的电影:{{name}}</view>
			<view class="content">
				<view v-for="(item,index) in arr" :key="index">
					<view class="left" @tap="img_nav(item.id)">
						<image :src="item.images.large" mode=""></image>
					</view>
					<view class="right">
						<view class="right_text">
							<text>{{item.title}}</text>
							<text>{{item.rating.average}}</text>
						</view>
						<text>{{item.title}}</text>
						<text>导演: {{item.directors[0].name}}</text>
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
				name: "",
				arr:[],
				start:1,
				count:10
			}
		},
		onLoad(obj) {
			this.name = obj.name
			this.url=obj.url
			this.req()
		},
		onReachBottom() {
			this.start+=this.count
			this.req()
		},
		methods: {
			req(){
				uni.request({
					url: this.url, //仅为示例，并非真实接口地址。
				    data:{
						 start:this.start,
						 count:this.count
					},
					success: (res) => {
						this.arr = this.arr.concat(res.data.subjects);
					}
				});
			}
		}
	}
</script>

<style>
	.main {
		padding: 20px;
	}


	.content>view {
		display: flex;
		justify-content: space-between;
		margin-top: 20px;
	}

	.left {
		width: 100px;
		height: 150px;
		border: 1px solid #eee;
	}

	.left>image {
		width: 100px;
		height: 150px;
	}

	.right {
		flex: 1;
		margin-left: 20px;
		display: flex;
		flex-direction: column;
	}

	.right_text {
		display: flex;
		justify-content: space-between;
	}

	.right_text>text:first-child {
		font-weight: bold;
		font-size: 20px;
	}

	.right_text>text:last-child {
		color: #B37188;
		font-size: 12px;
	}
</style>
