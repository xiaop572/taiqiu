<template>
	<view class="content">
		<image src="../../static/logo.png" mode="widthFix" class="logo"></image>
		<text class="title">台球会所</text>
		<button class="loginBtn" open-type="getUserInfo" @getuserinfo="getUserInfo">一键登录</button>
	</view>
</template>

<script>
	import {
		req
	} from '../../util/request.js'
	export default {
		data() {
			return {
				code: ""
			}
		},
		onLoad() {
			uni.login({
				success: (res) => {
					console.log(res)
					if (res.errMsg == "login:ok") {
						this.code = res.code;
					} else {
						uni.showToast({
							title: '系统异常，请联系管理员!'
						})
					}
				}
			})
		},
		methods: {
			getUserInfo(e) {
				uni.getProvider({
					service: 'oauth',
					success(res) {
						uni.getUserInfo({
							provider: res.provider[0],
							success(ress) {
								console.log(ress)
								uni.navigateTo({
									url:"../register/register"
								})
							}
						})
					}
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		width: 500rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 30rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	.loginBtn{
		width: 80%;
		color: #FFFFFF;
		background: #44652e;
		margin-top: 100rpx;
	}
</style>
