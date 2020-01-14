<template>
	<!-- 左边 w:373 h:530 右边:w:375 h 264 边h2 -->
	<view class="d-flex ">
		<image :src="resdata.big.src"
		lazy-load
		style="width: 373upx;height: 530upx;border-right: 2upx solid #F5F5F5;"
		></image>
		<view class="d-flex flex-column">
			<image :src="resdata.samlltop.src"
			style="width: 375upx;height: 264upx;border-bottom: 2upx solid #F5F5F5"
			></image>
			<image :src="resdata.samllbottom.src"
			style="width: 375upx;height: 264upx;"
			></image>
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Object
		}
	}
</script>

<style>
</style>
