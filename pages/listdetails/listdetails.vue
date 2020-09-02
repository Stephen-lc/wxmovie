<template>
	<view class="container">
		<view class="top"></view>

		<view class="center">

			<view class="center_top">
				<view class="center_left">
					<text>看过0部</text>
					<text> / 共250部</text>
				</view>
				<button size="mini">登录查看成就</button>
			</view>
			<view class="main" v-for="(item,index) in list" :key="index">
				<text>No.{{item.num}}</text>
				<view class="center_main">
					<view class="main_img">
						<image :src="item.images.large" mode=""></image>
					</view>
					<view class="main_text">
						<text>{{item.title}}</text>
						<view class="text_view">
							<uni-rate size="12" v-model="item.rating.average/2" />
							<text style="font-size: 12px;">{{item.rating.average}}</text>
						</view>
						<text>{{item.countries}} / {{item.genres}} / {{item.directors[0].name}}</text>
					</view>
					<view class="center_right">
						<text>看过</text>
					</view>
				</view>
				<view class="main_foot">
					
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
				list: [],
				value: 4,
				name:"",
			}
		},
		onLoad(obj) {
			// console.log(obj)
			this.name=obj.name
			uni.request({
				url: obj.src, //仅为示例，并非真实接口地址。
				success: (res) => {
					let num=1
					for(let obj of res.data.subjects){
						obj.num=num++
					}
					this.list = res.data.subjects;
					console.log(this.list)
				}
			});
		},
		methods: {
             
		},
		computed:{
			// getnum(){
			// 	let num=1
			// 	for(let obj of this.list){
			// 		num+=obj.num
			// 	}
			// 	return num
			// }
		},
	}
</script>

<style lang="less" scoped>
	.container{
		background-color: #ccc;
	}
	.top {
		width: 750rpx;
		height: 200px;
		background-color: #007AFF;
	}

	.center {
		
		padding:0 0 20px 0;


		.center_top {
			display: flex;
			padding: 20px;
			justify-content: space-between;
			align-items: center;
			background-color: #FFFFFF;

			.center_left {
				flex: 1;
				display: flex;
				justify-content: flex-start;
				align-items: center;

				text:last-child {
					color: #D3D3D3;
				}
			}

			button {
				background-color: #F6B05D;
				border-radius: 20px;
			}
		}

		>.main {
			margin-bottom: 20px;
			padding: 20px;
			background-color: #FFFFFF;
			>text {
				margin: 10px 0;
				display: inline-block;
				padding: 5px;
				font-size: 12px;
				background-color: #F6B05D;
				color: #A9741F;
				border-radius: 5px;
			}

			.center_main {
				display: flex;
				justify-content: space-between;

				.main_img {
					width: 100px;
					height: 150px;

					image {
						width: 100px;
						height: 150px;
					}
				}

				.main_text {
					flex: 1;
					margin: 0 10px;

					>text:first-child {
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
						align-items: center;
					}
				}

				.center_right {
					width: 100px;
					height: 150px;
					display: flex;
					align-items: center;
					justify-content: center;
					// background-color: #4CD964;
				}
			}
			.main_foot{
				width: 100%;
				padding: 20px;
				background-color: #F7F7F7;
			}

		}
	}
</style>
