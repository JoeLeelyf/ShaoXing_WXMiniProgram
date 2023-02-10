<template>
	<view class="login-container">
	<!-- 	<uni-icons type="contact-filled" size="100" color="#AFAFAF"></uni-icons> -->
		<button class="avatar-wrapper" open-type="chooseAvatar" bindchooseavatar="onChooseAvatar">
			<image class="avatar" :src="avatarUrl"></image>
		</button>

		<view class="name-box">
			<view class="name">昵称</view>
			<input type="nickname" class="weui-input" placeholder="请输入昵称"/>
		</view>


		
		<button type="primary" class="btn-login" @click="getUserProfile(e)">一键登录</button>
		<text class="tips-text"> 登录后享受更多权益</text>
	</view>
</template>

<script>
	import {mapMutations} from 'vuex'
	const defaultAvatarUrl = 'https://mmbiz.qpic.cn/mmbiz/icTdbqWNOwNRna42FI242Lcia07jQodd2FJGIYQfG0LAJGFxM4FbnQP6yfMxBgJ0F3YRqJCJ1aPAK2dQagdusBZg/0'
	export default {
		name:"my-login",

		data() {
			return {
				avatarUrl: defaultAvatarUrl
			};
		},
		methods: {
			...mapMutations('m_user',['updateUserInfo']),
			// 用户授权后，获取用户的基本信息
			getUserProfile(e) {
				uni.getUserProfile({
					desc: '你的授权信息',
					success: (res) => {
						this.updateUserInfo(res.userInfo)
						this.getToken(res)
					},
					fail: (res) => {
						return uni.$showMsg('您取消了授权')
					}
				})
			},
			async getToken(info) {
				// 获取 code 对应的值
				const [err, res] = await uni.login().catch(err => err)
				if(err || res.errMsg !== 'login:ok') return uni.$showMsg('登录失败！')
				
				// 准备参数
				const query = {
					code: res.code,
					encryptedData: info.encryptedData,
					iv: info.iv,
					rawData: info.rawData,
					signature: info.signature
				}
				
				const { data: loginResult } = await uni.$http.post('/api/public/v1/users/wxlogin', query)
				console.log(loginResult)
				if(loginResult.meta.status !== 200) return uni.$showMsg('登录失败！')
				uni.$showMsg('登陆成功！')
			},
			onChooseAvatar(e) {
			    const { avatarUrl } = e.detail 
			    this.setData({
			      avatarUrl,
			    })
					console.log(avatarUrl)
			}
		}
	}
</script>

<style lang="scss">
	.login-container {
		height: 750rpx;
		background-color: #f8f8f8;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		// position: relative;
		// overflow: hidden;
		// &::after {
		// 	content: ' ';
		// 	display: block;
		// 	width: 100%;
		// 	height: 40px;
		// 	background-color: white;
		// 	position: absolute;
		// 	bottom: 0;
		// 	left: 0;
		// 	border-radius: 100%;
		// 	transform: translateY(50%);
		// }
		
		.btn-login {
			width: 90%;
			border-radius: 100px;
			margin: 15px 0;
		}
		.tips-text {
			font-size: 12px;
			color: grey;
		}
	}
	
	.avatar-wrapper {
		padding: 0;
		width: 56px !important;
		border-radius: 8px;
		margin-top: 40px;
		margin-bottom: 40px;
	}
	.avatar {
		display: block;
		width: 56px;
		height: 56px;
	}
	.container {display: flex;}
	.name-box {
		display: flex;

		.name {
			padding-right: 20px;
			align-items: center;
			justify-content: center;
			font-size: 17px;
		}
	}
</style>