<template>
	<view class="container">
		<view class="top">
			<button type="default" size="mini">登录</button>
		</view>
		<view class="main">
			<view class="main_top">
				<text>我的书影音</text>
				<text>登录查看 ></text>
			</view>
			<view class="main_content">
				<view v-for="(item,index) in list" :key="index">
					<view class="content_left">
						<image :src="item.src" mode=""></image>
					</view>
					<view class="content_right">
						<view class="right_name">
							<text>{{item.name}}</text>
							<text>{{item.num}} 看过</text>
						</view>
						<view class="right_center">
							<text>标记10部影片</text>
							<text>标记10部影片</text>
						</view>
					    <view class="right_right">
					    	<button type="default" size="mini">立即开启</button>
							<text>></text>
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
				list:[
					{id:0,src:"../../static/adiou.png",name:"观影分析",num:0},
					{id:1,src:"../../static/book.png",name:"观影分析",num:0},
					{id:2,src:"../../static/music.png",name:"观影分析",num:0},
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="less" scoped>
 .top{
	 width: 750rpx;
	 height: 300px;
	 background-color: #007AFF;
	 display: flex;
	 justify-content: center;
	 align-items: center;
	 button{
		 width: 200px;
		 background-color: #FFFFFF;
		 text-align: center;
		 line-height: 50px;
		 font-size: 16px;
		 border-radius: 30px;
	 }
 }
 .main{
 		 padding: 10px 20px;
 		 .main_top{
 			 display: flex;
 			 justify-content: space-between;
 			 align-items: center;
 			 line-height: 24px;
			 text:first-child{
				 font-weight: bold;
				 font-size: 16px;
			 }
 		 }
		 .main_content{
			 >view{
				 display: flex;
				 justify-content: flex-start;
				 
				 .content_left{
					 padding: 20px 10px;
					 image{
						 width: 40px;
						 height: 40px;
						 margin-top: 10px;
					 }
				 }
				 .content_right{
					 flex: 1;
					 display: flex;
					 justify-content: space-between;
					 padding: 10px 0;
					 border-bottom: 1px solid #F7F7F7;
					 >view:not(:last-child){
						 display: flex;
						 flex-direction: column;
						 align-items: center;
					 }
					 .right_name{
						 text{
							 line-height: 34px;
							 color: #828282;
						 }
					 }
					 .right_center{
						 flex: 1;
						 margin-left: 40px;
						 display: flex;
						 justify-content: center;
						 font-size: 12px;
						 color: #D5D5D5;
					 }
					 .right_right{
						 display: flex;
						 justify-content: space-between;
						 align-items: center;
						 margin-left: 20px;
						 text{
							 margin-left: 10px;
							 font-size: 20px;
						 }
					 }
				 }
			 }
		 }
 }
</style>
