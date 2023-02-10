<template>
	<view>
	<my-search @click="gotoSearch"></my-search>
	<view class="cate">
		<button class="btn" type="default" @click="gotoPage('all')">全部</button>
		<button class="btn" type="default" @click="gotoPage('mine')">我的</button>
		<button class="btn" type="default" @click="gotoPage('query')">我要提问</button>
	</view>
	<my-qa-all v-if="flag === 'all'"></my-qa-all>
	<my-qa-mine v-else-if="flag === 'mine'"></my-qa-mine>
	<my-qa-query v-else-if="flag === 'query'"></my-qa-query>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				flag: 'all'
			};
		},
		methods: {
			gotoSearch() {
				uni.navigateTo({
					url: '/subpkg/search/search?from=qa'
				})
			},
			gotoPage(e) {
				this.flag = e
			}
		}
	}
</script>

<style lang="scss">
	.cate {
		display: flex;
		.btn {
			width: 33.33%;
		}
	}
</style>
