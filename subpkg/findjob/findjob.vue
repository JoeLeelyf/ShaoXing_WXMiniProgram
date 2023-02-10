<template>
	<view>
		<my-search bgcolor="#f4f4f4" radius="0" @click="gotoSearch"></my-search>
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
					url: '/subpkg/search/search?from=findjob'
				})
			}
		}
	}
</script>

<style lang="scss">

</style>
