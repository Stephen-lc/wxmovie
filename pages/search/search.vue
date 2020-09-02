<template>
	<view class="container">
		<view class="search">
			<input type="text" @confirm="search" v-model="value" placeholder="搜索" />
		</view>
		<view class="content">
			<view v-for="(item,index) in arr" :key="index">
				<view class="left" @tap="img_nav(item.id)">
					<image :src="item.images.large" mode=""></image>
				</view>
				<view class="right">
					<view class="right_text">
						<text class="tiem_title">{{item.title}}</text>
						<text>{{item.rating.average}}</text>
					</view>
					<text class="tiem_title">{{item.title}}</text>
					<text>导演: {{item.directors[0].name}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value:"",
				arr:[]
			}
		},
		methods: {
			search() {
				let value = this.value
				uni.request({
					url: 'http://t.yushu.im/v2/movie/search?apikey=0df993c66c0c636e29ecbb5344252a4a&q=' + value +
						'&start=0&count=10', //仅为示例，并非真实接口地址。
			
					success: (res) => {
						this.arr = res.data.subjects;
					}
				});
			}
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
	.content{
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
	.tiem_title{
		display: inline-block;
		width:150px;
		font-size: 14px;
		margin-bottom: 20px;
		overflow:hidden;
		text-overflow:ellipsis;
		white-space:nowrap;
	}
	.right_text>text:first-child {
		font-weight: bold;
		font-size: 16px;
	}
	
	.right_text>text:last-child {
		color: #B37188;
		font-size: 12px;
	}
</style>
