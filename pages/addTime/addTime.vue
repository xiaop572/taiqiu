<template>
	<view class="addTimeBox">
		<view class="timeList" @click="show=true">
			<text class="left">选择日期</text>
			<text>{{time}}</text>
		</view>
		<view class="timeList" @click="show1=true">
			<text class="left">开始时间</text>
			<text>{{startTime}}</text>
		</view>
		<view class="timeList" @click="show2=true">
			<text class="left">结束时间</text>
			<text>{{endTime}}</text>
		</view>
		<button class="submit" @click="submit">添加</button>
		<u-picker mode="time" v-model="show" :params="params" @confirm="confirm"></u-picker>
		<u-picker mode="time" v-model="show1" :params="params1" @confirm="confirm1"></u-picker>
		<u-picker mode="time" v-model="show2" :params="params1" @confirm="confirm2"></u-picker>
		<tab-bar></tab-bar>
	</view>
</template>

<script>
	import {
		baseUrl
	} from '../../util/config.js'
	import moment from 'moment'
	import tabBar from '../../components/tabbar/tabbar.vue'
	export default {
		components: {
			tabBar
		},
		data() {
			return {
				params: {
					year: true,
					month: true,
					day: true,
					hour: false,
					minute: false,
					second: false
				},
				params1: {
					year: false,
					month: false,
					day: false,
					hour: true,
					minute: true,
					second: false
				},
				time: "",
				startTime: "",
				endTime: "",
				show: false,
				show1: false,
				show2: false
			}
		},
		methods: {
			confirm(res) {
				this.time = `${res.year}-${res.month}-${res.day}`
			},
			confirm1(res) {
				this.startTime = `${res.hour}:${res.minute}`
			},
			confirm2(res) {
				this.endTime = `${res.hour}:${res.minute}`
			},
			submit(){
				uni.request({
					url:baseUrl+"/newapi/api/time/addfreetime",
					method:"POST",
					data:{
						riqi:this.time,
						sj1:this.startTime,
						sj2:this.endTime,
						openid:uni.getStorageSync("openid")
					},
					success: (res) => {
						if(res.data.status){
							uni.showToast({
							    title: '添加成功',
							    duration: 2000
							});
							setTimeout(()=>{
								uni.redirectTo({
									url:"../timeSuper/timeSuper"
								})
							},1500)
						}
					}
				})
			}
		},
		mounted() {
			this.time = moment().format('YYYY-MM-DD');
			this.startTime = "08:00";
			this.endTime = "08:00"
			
		}
	}
</script>

<style>
	page {
		background-color: #f2f2f2;
	}

	.addTimeBox {
		margin-top: 40rpx;
	}

	.timeList {
		padding: 40rpx 20rpx;
		background: #FFFFFF;
		margin-top: 20rpx;
	}

	.left {
		padding: 0 30rpx 0 20rpx;
	}
	.submit{
		background: #44652e;
		width: 80%;
		color: #FFFFFF;
		background: #44652e;
		margin-top: 100rpx;
	}
</style>
