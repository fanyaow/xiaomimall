<template>
	<view>
		<!-- 顶部选项卡 -->
		<scroll-view scroll-x class="border-bottom scroll-row " style="height: 80upx;" :scroll-into-view="scrollinto" scroll-with-animation>
			<view
				class="scroll-row-item px-3 "
				@click="changeTab(index)"
				style="height: 80upx;"
				v-for="(item, index) in tabBars"
				:key="index"
				:class="tabIndex === index ? 'main-text-color' : ''"
				:id="'tab' + index"
			>
				<text class="font-md">{{ item.name }}</text>
			</view>
		</scroll-view>
		<swiper :duration="150" :current="tabIndex" :style="'height:' + scrollH + 'px;'" @change="onChangeTab">
			<swiper-item v-for="(item, index) in newsitems" :key="index">
				<scroll-view scroll-y="true" :style="'height:' + scrollH + 'px;'" 
				@scrolltolower="loadmore(index)">
					<block v-for="(list,listIndex) in item.list" :key="listIndex">
						<!-- 轮播图组件 -->
						<swiper-image v-if="list.type === 'swiper'" :resdata="list.data"></swiper-image>
						<!-- 分类图标组件 -->
						<template v-else-if="list.type === 'indexnavs'">
							<index-nav  :resdata="list.data"></index-nav>
							<!-- 分割线组件 -->
							<divider></divider>
						</template>
						<template v-else-if="list.type === 'threeadv'">
							<three-adv  :resdata="list.data"></three-adv>
							<divider />
						</template>
						<!-- 三图片广告展示 -->
						
						<!-- 基础卡片组件 -->
						<!-- <card headTitle="每日精选" bodyCover="/static/images/demo/demo4.jpg"></card> -->
						<!-- 扩展 -->
						<!-- <card :showhead="false">
							<block slot='title'>每日精选</block>
							<image src="/static/images/demo/demo4.jpg" mode="widthFix"></image>
						</card> -->

						<!-- 公共列表组件 -->
						<view class="row j-sb" v-else-if="list.type === 'list'">
							<block v-for="(item2, index2) in list.data" :key="index2">
								<common-list :item="item2" :index="index2" />
							</block>
						</view>
					</block>
					<!-- 上拉加载更多 -->
					<divider style="height: 10upx;"/>
					<view class="d-flex a-center j-center text-light-muted font-md py-3">
						上拉加载更多
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	// 模拟后端数据库
let demotabBar = [
	{ name: '推荐' },
	{ name: '体育' },
	{ name: '科技' },
	{ name: '财经' },
	{ name: '新闻' },
	{ name: '历史' },
	{ name: '军事' },
	{ name: '电脑' },
	{ name: '电影' },
	{ name: '图书' }
];
let demo1 = [
	{
		type:"swiper",
		data:[
				{ src: '../../static/images/demo/demo4.jpg' },
				{ src: '../../static/images/demo/demo4.jpg' },
				{ src: '../../static/images/demo/demo4.jpg' },
			]
	},
	{
		type:"indexnavs",
		data:[
				{ src: '../../static/indexnav/1.png', name: '新品分类' },
				{ src: '../../static/indexnav/2.gif', name: '小米众筹' },
				{ src: '../../static/indexnav/3.gif', name: '以旧换新' },
				{ src: '../../static/indexnav/4.gif', name: '1分拼团' },
				{ src: '../../static/indexnav/5.gif', name: '超值特卖' },
				{ src: '../../static/indexnav/6.gif', name: '小米秒杀' },
				{ src: '../../static/indexnav/7.gif', name: '真心想要' },
				{ src: '../../static/indexnav/8.gif', name: '电视热卖' },
				{ src: '../../static/indexnav/9.gif', name: '家电热卖' },
				{ src: '../../static/indexnav/10.gif', name: '米粉卡' }
			]
	},
	{
		type:"threeadv",
		data:{
			big: { src: '/static/images/demo/demo1.jpg' },
			samlltop: { src: '/static/images/demo/demo2.jpg' },
			samllbottom: { src: '/static/images/demo/demo10.jpg' }
		}
	},
	{
		type:"list",
		data:[
			{
				cover: '/static/images/demo/list/1.jpg',
				title: '米家空调',
				desc: '1.5变频空调',
				oprice: 2699,
				pprice: 1699
			},
			{
				cover: '/static/images/demo/list/3.jpg',
				title: '米家空调',
				desc: '1.5变频空调',
				oprice: 2699,
				pprice: 1699
			}
		]
	}
];
let demo2= [{
		type:"swiper",
		data:[
				{ src: '../../static/images/demo/demo4.jpg' },
				{ src: '../../static/images/demo/demo4.jpg' },
				{ src: '../../static/images/demo/demo4.jpg' },
			]
	},
	{
		type:"indexnavs",
		data:[
				{ src: '../../static/indexnav/6.gif', name: '小米秒杀' },
				{ src: '../../static/indexnav/7.gif', name: '真心想要' },
				{ src: '../../static/indexnav/8.gif', name: '电视热卖' },
				{ src: '../../static/indexnav/9.gif', name: '家电热卖' },
				{ src: '../../static/indexnav/10.gif', name: '米粉卡' }
			]
	},
	{
		type:"list",
		data:[
			{
				cover: '/static/images/demo/list/1.jpg',
				title: '米家空调',
				desc: '1.5变频空调',
				oprice: 2699,
				pprice: 1699
			},
			{
				cover: '/static/images/demo/list/3.jpg',
				title: '米家空调',
				desc: '1.5变频空调',
				oprice: 2699,
				pprice: 1699
			}
		]
	}];
import swiperImage from '@/components/index/swiper-image.vue';
import indexNav from '@/components/index/index-nav.vue';
import threeAdv from '@/components/index/three-adv.vue';
import card from '@/components/common/card.vue';
import commonList from '@/components/common/common-list.vue';
export default {
	components: {
		swiperImage,
		indexNav,
		threeAdv,
		card,
		commonList
	},
	data() {
		return {
			scrollinto: '',
			scrollH: 500,
			tabIndex: 0,
			tabBars: [],
			newsitems: []
		};
	},
	onLoad() {
		//获取可视区域高度
		uni.getSystemInfo({
			success: res => {
				this.scrollH = res.windowHeight - uni.upx2px(80);
			}
		})
		// 初始化数据
		this.__init()
	},
	methods: {
		// 初始化数据
		__init(){
			// 获取顶部选项卡
			this.tabBars=demotabBar
			// 根据顶部选项卡生成页面
			let arr=[]
			for (var i = 0; i < this.tabBars.length; i++) {
				let obj = {
					list:[],
					//1.上拉加载更多,2.加载中....3,没有更多
					loadtext:'上拉加载更多'
				}
				// 获取首屏数据
				if (i === 0){
					obj.list=demo1
				}
				arr.push(obj)
			}
			this.newsitems = arr
		},
		// 切换选项卡 
		changeTab(index) {
			if (this.tabIndex === index) {
				return;
			}
			this.tabIndex = index;
			this.scrollinto = 'tab' + index;
			this.addData()
		},
		//监听滑动
		onChangeTab(e) {
			this.changeTab(e.detail.current);
		},
		// 加载数据
		addData(){
			// 取当前索引
			let index = this.tabIndex
			// 请求数据库
			this.newsitems[index].list=demo2
		},
		loadmore(index){
			let item =this.newsitems[index]
			// 判断是否处于可加载状态
			if (item.loadtext !=='上拉加载更多') return;
			// 模拟加载
			item.loadtext = '加载中...'
			setTimeout(()=>{
				//加载数据
				item.list=[...item.list,...demo2];
			//恢复状态
				item.loadtext = '上拉加载更多'
			},5000);
		}
	}
}

</script>

<style></style>
