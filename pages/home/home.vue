<template>
	<view>
		<!-- 轮播图区域 -->
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
			<swiper-item v-for="(item, i) in swiperList" :key="i">
				<view class="swiper-item">
					<image
						src="https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/2f4c023e17bb80477294b60c43569c12.jpeg?sign=210c58b63b66229959f304d1bcd83183&t=1676068065">
					</image>
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
				<swiper class="notice-swiper" :autoplay="true" :interval="3000" :duration="1000" circular="true"
					vertical="true">
					<swiper-item v-for="(item, i) in noticeList" :key="i">
						<view class="notice-item">《绍兴市人力资源和社会保障局关于印发〈绍兴市职业技能培训指导规程（试行）〉的通知》的政策解读</view>
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
					<view class="gongxu-item" v-for="(item, i) in gongxuList" :key="i"
						@click="gongxuClickHandler(item)">
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
					<view class="center-item" v-for="(item, i) in centerList" :key="i"
						@click="centerClickHandler(item)">
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
				const {
					data: res
				} = await uni.$http.get('/api/public/v1/home/swiperdata')
				// 请求失败
				if (res.meta.status !== 200) return uni.$showMsg()
				// 成功
				this.swiperList = res.message
			},
			async getNoticeList() {
				const {
					data: res
				} = await uni.$http.get('/api/public/v1/goods/qsearch', {
					query: 'a'
				})
				// 请求失败
				if (res.meta.status !== 200) return uni.$showMsg()
				// 成功
				this.noticeList = res.message
			},
			async getGongxuList() {
				const {
					data: res
				} = await uni.$http.get('/api/public/v1/home/catitems')
				if (res.meta.status !== 200) return uni.$showMsg()
				this.gongxuList = res.message
				this.gongxuList[0].image_src='https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/%E6%9C%AA%E6%A0%87%E9%A2%98-1.jpg?sign=b86b756bba3ee4758d0afd29825e6616&t=1676275697'
				this.gongxuList[1].image_src='https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/%E4%BC%81%E4%B8%9A.png?sign=7a836395e6ffdc45f47e1ea4a05a24a2&t=1676069067'
				this.gongxuList[2].image_src='https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/%E4%BA%BA%E6%89%8D%E6%B5%81%E5%8A%A8%E3%80%81%E4%BA%BA%E6%89%8D%E5%87%BA%E5%85%A5%E5%A2%83.png?sign=8e961dead4a7e476a2085c1bd326880d&t=1676069176'
				this.gongxuList[3].image_src='https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/%E6%8A%80%E6%9C%AF%E6%9C%8D%E5%8A%A1.png?sign=eb6d82e8b985f195cea9ca2f8dd8810d&t=1676069157'
				this.gongxuList[0].name = '找政策'
				this.gongxuList[1].name = '找工作'
				this.gongxuList[2].name = '找人才'
				this.gongxuList[3].name = '找技术'
			},
			async getCenterList() {
				const {
					data: res
				} = await uni.$http.get('/api/public/v1/home/catitems')
				if (res.meta.status !== 200) return uni.$showMsg()
				this.centerList = res.message.splice(0, 3)
				this.centerList[0].image_src='https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/%E5%9C%B0%E5%9B%BE%20(1).png?sign=7f231059eeeed44507fa7f5d9f3fe83d&t=1676069228'
				this.centerList[1].image_src='https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/%E5%9C%B0%E5%9B%BE.png?sign=ce35f5eee11a1fd03bcb07fa84cca8c6&t=1676069237'
				this.centerList[2].image_src='https://prod-6g0a1d1h5dcb92d9-1308482024.tcloudbaseapp.com/icon/%E9%A2%84%E7%BA%A6.png?sign=0aaee884179d86251cc3f4d3c7e056e0&t=1676069264'
				this.centerList[0].name = '站点地图'
				this.centerList[1].name = '站点查询'
				this.centerList[2].name = '预约'
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
						width: 75%;
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
						width: 60%;
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
