<template>
	<view class="card">
		<!-- head -->
		<view v-if="showhead" class="font-md font-weight p-2 border-bottom main-border-color">
			<slot name="title">
				<text v-if="headTitle" class="font-md font-weight">{{headTitle}}</text>
			</slot>
			
		</view>
		<!-- body -->
		<image v-if="bodyCover" :src="bodyCover" mode="widthFix"></image>
		<slot></slot>
	</view>
</template>

<script>
	export default{
		props:{
			//头部标题
			headTitle:String,
			//封面图
			bodyCover:String,
			//是否显示头部
			showhead:{
				type:Boolean,
				default:true
			}
		}
	}
</script>

<style>
</style>
