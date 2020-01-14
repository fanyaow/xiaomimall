<template>
	<view>
		<!-- 轮播图组件 -->
		<swiper-image :resdata="swipers"></swiper-image>
	    <!-- 分类图标组件 -->
		<index-nav :resdata="indexnavs"></index-nav>
		<!-- 分割线组件 -->
		<divider></divider>
		<!-- 三图片广告展示 -->
		<three-adv :resdata="threeadv"></three-adv>
		<divider />
		<!-- 基础卡片组件 -->
		<card headTitle="每日精选" bodyCover="/static/images/demo/demo4.jpg"></card>
		<!-- 扩展 -->
		<!-- <card :showhead="false">
			<block slot='title'>每日精选</block>
			<image src="/static/images/demo/demo4.jpg" mode="widthFix"></image>
		</card> -->
		
		<!-- 公共列表组件 -->
		<view class="row j-sb">
			<block v-for="(item,index) in commonList" :key="index">
				<common-list :item="item" :index="index"></common-list>
			</block>
		</view>
		
	</view>
</template>

<script>
	import swiperImage from '@/components/index/swiper-image.vue';
	import indexNav from "@/components/index/index-nav.vue";
	import threeAdv from "@/components/index/three-adv.vue";
	import card from "@/components/common/card.vue";
	import commonList from "@/components/common/common-list.vue"
	export default {
		components:{
			swiperImage,
			indexNav,
			threeAdv,
			card,
			commonList
		},
		data() {
			return {
				swipers:[
					{src:"../../static/images/demo/demo4.jpg"},
					{src:"../../static/images/demo/demo4.jpg"},
					{src:"../../static/images/demo/demo4.jpg"}
				],
				indexnavs:[
					{ src:"../../static/indexnav/1.png", name:"新品分类" },
					{ src:"../../static/indexnav/2.gif", name:"小米众筹" },
					{ src:"../../static/indexnav/3.gif", name:"以旧换新" },
					{ src:"../../static/indexnav/4.gif", name:"1分拼团" },
					{ src:"../../static/indexnav/5.gif", name:"超值特卖" },
					{ src:"../../static/indexnav/6.gif", name:"小米秒杀" },
					{ src:"../../static/indexnav/7.gif", name:"真心想要" },
					{ src:"../../static/indexnav/8.gif", name:"电视热卖" },
					{ src:"../../static/indexnav/9.gif", name:"家电热卖" },
					{ src:"../../static/indexnav/10.gif", name:"米粉卡" }
				],
				threeadv:
					{
						big:{src:"/static/images/demo/demo1.jpg"},
						samlltop:{src:"/static/images/demo/demo2.jpg"},
						samllbottom:{src:"/static/images/demo/demo10.jpg"},
					},
				commonList:[
					{
						cover:"/static/images/demo/list/1.jpg",
						title:"米家空调",
						desc:"1.5变频空调",
						oprice:2699,
						pprice:1699
					},
					{
						cover:"/static/images/demo/list/3.jpg",
						title:"米家空调",
						desc:"1.5变频空调",
						oprice:2699,
						pprice:1699
					}
				]
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	
</style>
