<template>
	<view>
		<my-search bgcolor="#ffffff" radius="0" @click="gotoSearch"></my-search>
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
					url: '/subpkg/search/search?from=findpolicy'
				})
			}
		}
	}
</script>

<style lang="scss">

</style>
