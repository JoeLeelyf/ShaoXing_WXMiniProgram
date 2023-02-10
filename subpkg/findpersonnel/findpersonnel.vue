<template>
	<view>
		<view class="topcol">
			<my-search class="search-box" bgcolor="#efefef" radius="18" @click="gotoSearch"></my-search>
			<view class="select-box" @click="gotoSelect">
				<uni-icons type="list" size="30"></uni-icons>
				<view class="select">筛选</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods: {
			gotoSearch() {
				uni.navigateTo({
					url: '/subpkg/search/search?from=findpersonnel'
				})
			},
			gotoSelect() {
				
			}
		}
	}
</script>

<style lang="scss">
	.topcol {
		display: flex;
		.search-box {
			width: 90%;
		}
		.select-box {
			display: flex;
			flex-direction: column;
			padding: 30px,10px;
		}
	}
</style>
