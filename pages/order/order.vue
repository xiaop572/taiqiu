<template>
	<view>
		<u-tabs-swiper ref="uTabs" :list="list" :current="current" @change="tabsChange" :is-scroll="false" swiperWidth="750"></u-tabs-swiper>
		<swiper :current="swiperCurrent" @transition="transition" @animationfinish="animationfinish">
			<swiper-item class="swiper-item">
				<scroll-view scroll-y style="height: 800rpx;width: 100%;" @scrolltolower="onreachBottom">
					<view class="orderList">
						<text class="ordeCode">订单号:312312313</text>
						<text class="phone">手机号:18857731771</text>
						<text class="peiLabel">陪练时间</text>
						<text class="time">14:00-16:00</text>
						<button class="jieBtn">接单</button>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item class="swiper-item">
				<scroll-view scroll-y style="height: 800rpx;width: 100%;" @scrolltolower="onreachBottom">
					<view class="orderList">
						<text class="ordeCode">订单号:312312313</text>
						<text class="phone">手机号:18857731771</text>
						<text class="peiLabel">陪练时间</text>
						<text class="time">14:00-16:00</text>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item class="swiper-item">
				<scroll-view scroll-y style="height: 800rpx;width: 100%;" @scrolltolower="onreachBottom">
					<view class="orderList">
						<text class="ordeCode">订单号:312312313</text>
						<text class="phone">手机号:18857731771</text>
						<text class="peiLabel">陪练时间</text>
						<text class="time">14:00-16:00</text>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [{
					name: '待接单'
				}, {
					name: '历史订单'
				}, {
					name: '爽约订单',
					cate_count: 5
				}],
				current: 0, // tabs组件的current值，表示当前活动的tab选项
				swiperCurrent: 0, // swiper组件的current值，表示当前那个swiper-item是活动的
			}
		},
		methods: {
			// tabs通知swiper切换
			tabsChange(index) {
				this.swiperCurrent = index;
			},
			// swiper-item左右移动，通知tabs的滑块跟随移动
			transition(e) {
				let dx = e.detail.dx;
				this.$refs.uTabs.setDx(dx);
			},
			// 由于swiper的内部机制问题，快速切换swiper不会触发dx的连续变化，需要在结束时重置状态
			// swiper滑动结束，分别设置tabs和swiper的状态
			animationfinish(e) {
				let current = e.detail.current;
				this.$refs.uTabs.setFinishCurrent(current);
				this.swiperCurrent = current;
				this.current = current;
			},
			// scroll-view到底部加载更多
			onreachBottom() {

			}
		}
	}
</script>

<style lang="less">
	.orderList{
		height: 240rpx;
		padding:30rpx;
		border-bottom: 1px solid #eee;
		position: relative;
		.ordeCode{
			display: block;
			font-size: 32rpx;
			color: #333;
		}
		.phone{
			display: block;
			margin-top: 10rpx;
			font-size: 28rpx;
			color: #333;
		}
		.peiLabel{
			display: block;
			margin-top:10rpx;
			font-size: 28rpx;
			color: #333;
		}
		.time{
			display: block;
			margin-top:10rpx;
			font-size: 28rpx;
			color: #333;
		}
		.jieBtn{
			width: 200rpx;
			height: 72rpx;
			line-height: 72rpx;
			font-size: 30rpx;
			position: absolute;
			bottom: 20rpx;
			right: 20rpx;
			background-color: #C83C3C;
			color: #fff;
		}
	}
	.orderList:first-child{
		border-top: 1px solid #eee;
	}
</style>
