<template>
	<view class="Home">
		<image src="../../static/zpInfo.jpg" alt="" mode="widthFix" class="zpInfo">
		<view class="list">
			<view @click="rTimeMan">
				<image src="../../static/gongshi.png" mode="widthFix"></image>
				<text>时间管理</text>
			</view>
			<view>
				<image src="../../static/tuijian.png" mode="widthFix" @click="rRecommend"></image>
				<text>待接单</text>
			</view>
			<view @click="rMyRecommend">
				<image src="../../static/zhaopin.png" mode="widthFix"></image>
				<text>历史订单</text>
			</view>
		</view>
		<tab-bar></tab-bar>
	</view>
</template>

<script>
	import tabBar from '../../components/tabbar/tabbar.vue'
	export default {
		components: {
			tabBar
		},
		methods:{
			rTimeMan(){
				uni.navigateTo({
					url:"../timeSuper/timeSuper"
				})
			},
			rRecommend(){
				uni.navigateTo({
					url:"../recommend/recommend"
				})
			},
			rMyRecommend(){
				uni.navigateTo({
					url:'../myRecommend/myRecommend'
				})
			},
			rCheck(){
				uni.navigateTo({
					url:'../check/check'
				})
			}
		}
	}
</script>

<style lang="less">
	.list {
		clear: both;
		overflow: hidden;
		margin-top: 80rpx;
		view {
			width: 33%;
			float: left;
			text-align: center;
			image{
				width: 50%;
				
			}
			text{
				display: block;
				font-size: 32rpx;
			}
		}
	}
	.zpInfo{
		width: 100%;
		margin:0 auto 0 auto;
		display: block;
	}
</style>
