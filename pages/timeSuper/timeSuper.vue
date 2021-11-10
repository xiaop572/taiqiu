<template>
	<view>
		<view class="caption">
			空闲时间
		</view>
		<u-swipe-action :show="item.show" :index="index" v-for="(item, index) in list" :key="item.id" @click="click"
			@open="open" :options="options">
			<view class="item u-border-bottom">
				<!-- 此层wrap在此为必写的，否则可能会出现标题定位错误 -->
				<view class="list">
					<text class="date">{{ item.date }}</text>
					<text class="time">{{ item.time }}</text>
				</view>
			</view>
		</u-swipe-action>
		<tab-bar></tab-bar>
		<view class="add" @click="rAddTime">
			<image src="../../static/add.png" mode="widthFix"></image>
		</view>
	</view>
</template>

<script>
	import tabBar from '../../components/tabbar/tabbar.vue'
	export default {
		components: {
			tabBar
		},
		data() {
			return {
				list: [{
					id: 1,
					date: '2021-12-31',
					time: '13:00-16:00',
					show: false
				}, {
					id: 1,
					date: '2021-12-31',
					time: '13:00-16:00',
					show: false
				}, ],
				disabled: false,
				btnWidth: 180,
				show: false,
				options: [
					{
						text: '删除',
						style: {
							backgroundColor: '#dd524d'
						}
					}
				]
			};
		},
		methods: {
			rAddTime(){
				uni.navigateTo({
					url:"../addTime/addTime"
				})
			},
			click(index, index1) {
				console.log(index)
			},
			// 如果打开一个的时候，不需要关闭其他，则无需实现本方法
			open(index) {
				// 先将正在被操作的swipeAction标记为打开状态，否则由于props的特性限制，
				// 原本为'false'，再次设置为'false'会无效
				this.list[index].show = true;
				this.list.map((val, idx) => {
					if (index != idx) this.list[idx].show = false;
				})
			}
		}
	};
</script>

<style>
	page {
		background: #f2f2f2;
	}

	.caption {
		font-size:30rpx;
		padding: 30rpx 0 0 20rpx;
		margin-bottom: 30rpx;
	}

	.list {
		background: #FFFFFF;
		padding: 30rpx;
	}

	.list .date {
		font-size: 30rpx;
		color: #333333;
	}

	.list .time {
		color: #999;
		margin-left: 20rpx;
	}

	.item {
		display: flex;
	}
	.add{
		background: #c13b3b;
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		position: fixed;
		right: 20rpx;
		bottom: 140rpx;
	}
	.add image{
		width: 60rpx;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		margin: auto;
		position: absolute;
	}
</style>
