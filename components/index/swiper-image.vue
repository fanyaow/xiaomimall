<template>
	<view>
		<!-- 轮播图  图片比例  750/350 -->
		<swiper indicator-dots autoplay :interval="5000" :duration="1000" circular>
			<block v-for="(item,index) in resdata" :key="index">
				<swiper-item>
					<view class="swiper-item" @tap="event(item)">
						<image :src="item.src" lazy-load style="height: 400upx;"></image>
					</view>
				</swiper-item>
			</block>
		</swiper>
	</view>
</template>

<script>
	export default {
		props:{
			resdata:Array
		},
		methods:{
			event(item){
				console.log('点击了轮播图')
			}
		}
	}
</script>

<style>
</style>
