<template>
	<view>
		<!-- 顶部选项卡 -->
		<scroll-view scroll-x class="border-bottom scroll-row " style="height: 80upx;" 
		:scroll-into-view="scrollinto" scroll-with-animation>
			<view class="scroll-row-item px-3 " @click="changeTab(index)"
			style="height: 80upx;" v-for="(item,index) in tabBars" :key='index'
			:class="tabIndex === index ? 'main-text-color':''" :id="'tab'+index">
				<text class="font-md">{{item.name}}</text>
			</view>
		</scroll-view>
		<swiper :duration="150" :current="tabIndex" :style="'height:'+scrollH+'px;'"
		@change="onChangeTab">
			<swiper-item v-for="(item,index) in tabBars" :key="index">
				<scroll-view scroll-y="true" :style="'height:'+scrollH+'px;'">
					
				
		
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
						<block v-for="(item,list) in commonList" :key="list">
							<common-list :item="item" :index="list"></common-list>
						</block>
					</view>
					
				</scroll-view>
			</swiper-item>
		</swiper>
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
				scrollinto:"",
				scrollH:500,
				tabIndex:0,
				tabBars:[
					{name:'推荐'},
					{name:'体育'},
					{name:'科技'},
					{name:'财经'},
					{name:'新闻'},
					{name:'历史'},
					{name:'军事'},
					{name:'电脑'},
					{name:'电影'},
					{name:'图书'}
				],
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
			//获取可视区域高度
			uni.getSystemInfo({
				success: (res) => {
					this.scrollH=res.windowHeight - uni.upx2px(80)
					
				}
			})
		},
		methods: {
			// 切换选项卡
			changeTab(index){
				if (this.tabIndex === index){
					return;
				}
				this.tabIndex = index
				this.scrollinto="tab"+index
			},
			//监听滑动
			onChangeTab(e){
				this.changeTab(e.detail.current)
			}
		}
	}
</script>

<style>
	
</style>
