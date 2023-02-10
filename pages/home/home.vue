<template>
	<view>
		<!-- 轮播图区域 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
			<swiper-item v-for="(item, i) in swiperList" :key="i">
				<view class="swiper-item">
					<image :src="item.image_src"></image>
				</view>
			</swiper-item>
		</swiper>
		
		<!-- 搜索区域 -->
		<view class="search-box">
			<my-search @click="gotoSearch"></my-search>
		</view>
		
		<!-- 公告栏 -->
		<view class="notice-container">
			<view class="notice-box">
				<uni-icons type="sound" size="18"></uni-icons>
				<text class="placeholder">公告：</text>
				<swiper class="notice-swiper" :autoplay="true" :interval="3000" :duration="1000" circular="true" vertical="true">
					<swiper-item v-for="(item, i) in noticeList" :key="i">
						<view class="notice-item">{{item.goods_name}}</view>
					</swiper-item>
				</swiper>
			</view>
		</view>
		
		<!-- 供需平台 -->
		<view class="gongxu-container">
			<view class="gongxu-box">
				<view class="icons-box">
					<uni-icons type="paperplane" size="17"></uni-icons>
					<text class="placeholder">供需平台</text>
				</view>
				<view class="gongxu-list">
					<view class="gongxu-item" v-for="(item, i) in gongxuList" :key="i" @click="gongxuClickHandler(item)">
						<image :src="item.image_src" class="gongxu-img" mode="widthFix"></image>
						<!-- 需要一个中文名和英文名 -->
						<text class="placeholder">{{item.name}}</text>
					</view>
				</view>
			</view>
		</view>
		
		<!-- 人才服务中心 -->
		<view class="center-container">
			<view class="center-box">
				<view class="icons-box">
					<uni-icons type="home" size="17"></uni-icons>
					<text class="placeholder">人才服务中心</text>
				</view>
				<view class="center-list">
					<view class="center-item" v-for="(item, i) in centerList" :key="i" @click="centerClickHandler(item)">
						<image :src="item.image_src" class="center-img" mode="widthFix"></image>
						<!-- 需要一个中文名和英文名 -->
						<text class="placeholder">{{item.name}}</text>
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
				// 轮播图的数据列表
				swiperList: [],
				// 公告栏的数据表
				noticeList: [],
				// 供需平台图片列表
				gongxuList: [],
				// 人才服务中心图片列表
				centerList: []
			};
		},
		
		onLoad() {
			// 获取轮播图
			this.getSwiperList()
			// 获取公告栏的公告
			this.getNoticeList()
			// 获取供需平台的图片
			this.getGongxuList()
			// 获取人才服务中心的图片
			this.getCenterList()
		},
		
		methods: {
			async getSwiperList() {
				const {data: res} = await uni.$http.get('/api/public/v1/home/swiperdata')
				// 请求失败
				if(res.meta.status !== 200) return uni.$showMsg()
				// 成功
				this.swiperList = res.message
			},
			async getNoticeList() {
				const {data: res} = await uni.$http.get('/api/public/v1/goods/qsearch', {query:'a'})
				// 请求失败
				if(res.meta.status !== 200) return uni.$showMsg()
				// 成功
				this.noticeList = res.message
			},
			async getGongxuList() {
				const {data: res} = await uni.$http.get('/api/public/v1/home/catitems')
				if(res.meta.status !== 200) return uni.$showMsg()
				this.gongxuList = res.message
				this.gongxuList[0].name = 'findpolicy'
				this.gongxuList[1].name = 'findjob'
				this.gongxuList[2].name = 'findpersonnel'
				this.gongxuList[3].name = 'findtech'
			},
			async getCenterList() {
				const {data: res} = await uni.$http.get('/api/public/v1/home/catitems')
				if(res.meta.status !== 200) return uni.$showMsg()
				this.centerList = res.message.splice(0, 3)
				this.centerList[0].name = 'map'
				this.centerList[1].name = 'query'
				this.centerList[2].name = 'appointment'
			},
			gotoSearch() {
				uni.navigateTo({
					url: '/subpkg/search/search?from=home'
				})
			},
			gongxuClickHandler(item) {
				uni.navigateTo({
					url: '/subpkg/' + item.name + '/' + item.name
				})
			},
			centerClickHandler(item) {
				uni.navigateTo({
					url: '/subpkg' + item.name + '/' + item.name
				})
			}
		}
	}
</script>

<style lang="scss">
	swiper {
		height: 330rpx;
		.swiper-item,
		image {
			width: 100%;
			height: 100%;
		}
		
	}
	
	.notice-container {
		background-color: #2b4b6b;
		height: 40px;
		padding: 0 10px;

		.notice-box {
			height: 36px;
			background-color: #ffffff;
			border-radius: 10px;
			padding: 0 5px;
			width: 100%;
			display: flex;
			align-items: center;
			white-space: nowrap;
			font-size: 15px;
			
			.notice-swiper {
				height: 36px;
				width: 100%;
				.notice-item {
					overflow: hidden;
					text-overflow: ellipsis;
					line-height: 36px;
					font-size: 15px;
				}
			}
		}
	}
	
	.gongxu-container {
		background-color: #2b4b6b;
		height: 160px;
		padding: 10px 10px;

		.gongxu-box {
			height: 150px;
			background-color: #ffffff;
			border-radius: 10px;
			padding: 0 5px;
			.gongxu-list {
				display: flex;
				
				.gongxu-item {
					width: 25%;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					.gongxu-img {
						width: 100%;
					}
				}
			}
		}
	}
	
	.center-container {
		background-color: #2b4b6b;
		height: 160px;
		padding: 10px 10px;
		.center-box {
			height: 150px;
			background-color: #ffffff;
			border-radius: 10px;
			padding: 0 5px;
			.center-list {
				display: flex;
				.center-item {
					width: 33.33%;
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					.center-img {
						width: 80%;
					}
					
				}
			}
		}
	}
	
	.placeholder {
	  font-size: 15px;
		margin-left: 5px;
		margin-right: 5px;
	}
	
</style>
