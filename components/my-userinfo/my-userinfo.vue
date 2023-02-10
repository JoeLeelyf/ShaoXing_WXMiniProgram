<template>
	<view class="my-userinfo-container">
		<!-- 头像和昵称区域 -->
		<view class="top-box">
			<image :src="userinfo.avatarUrl" class="avater"></image>
			<view class="nickname">{{userinfo.nickName}}</view>
		</view>
		
		<!-- 第二个区域 -->
		<view class="panel-box">
			<view class="panel-body">
				<view class="panel-item">
					<image src="../../static/mycenter_icons/c1.png" class="icon"></image>
					<text>消息提醒</text>
				</view>
				<view class="panel-item">
					<image src="../../static/mycenter_icons/c2.png" class="icon"></image>
					<text>我的简历</text>
				</view>
				<view class="panel-item">
					<image src="../../static/mycenter_icons/c3.png" class="icon"></image>
					<text>人才认定</text>
				</view>
			</view>
		</view>
		
		<!-- 第三个区域 -->
		<view class="panel">
			<view class="panel-list-item">
				<view class="info">
					<uni-icons type="person" size="20"></uni-icons>
					<text>个人信息</text>
				</view>
				<uni-icons type="arrowright" size="15" class="icon"></uni-icons>
			</view>
			<view class="panel-list-item">
				<view class="info">
					<uni-icons type="wallet" size="20"></uni-icons>
					<text>电子人才证</text>
				</view>
				<uni-icons type="arrowright" size="15"></uni-icons>
			</view>
			<view class="panel-list-item">
				<view class="info">
					<uni-icons type="star" size="20"></uni-icons>
					<text>我的收藏</text>
				</view>
				<uni-icons type="arrowright" size="15"></uni-icons>
			</view>
			<view class="panel-list-item">
				<view class="info">
					<uni-icons type="info" size="20"></uni-icons>
					<text>隐私条款</text>
				</view>
				<uni-icons type="arrowright" size="15"></uni-icons>
			</view>
		</view>
	</view>
</template>

<script>
	import {mapState} from 'vuex'
	
	export default {
		name:"my-userinfo",
		data() {
			return {
				
			};
		},
		computed: {
			...mapState('m_user', ['userinfo'])
		}
	}
</script>

<style lang="scss">
	.my-userinfo-container {
		height: 100%;
		// background-color: #f4f4f4;
		background-color: #2b4b6b;
		align-items: center;
		justify-content: center;
		
		.top-box {
			height: 400rpx;
			background-color: #2b4b6b;
			display: flex;
			justify-content: center;
			align-items: center;
			flex-direction: column;
			.avatar {
				width: 90px;
				height: 90px;
				border-radius: 45px;
				border: 2px solid #FFF;
				box-shadow: 0 1px 5px black;
			}
			.nickname {
				font-size: 16px;
				color: #FFF;
				font-weight: bold;
				margin-top: 10px;
			}
		}
		.panel-box{

			padding: 0 20px;
			
		.panel-body {
			background-color: #ffffff;
			border-radius: 15px;
			display: flex;
			justify-content: space-around; 
			align-items: center;
			.panel-item {
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: space-around;
				padding: 10px 0;
				font-size: 13px;
				.icon {
					width: 35px;
					height: 35px;
				}
			}
			}
		}
	}
	.panel{
		background-color: #ffffff;
		border-radius: 10px;
	.panel-list-item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		font-size: 15px;
		padding: 0 10px;
		line-height: 45px;

		
		
	}
	}
</style>