<template>
	<view class="content">
		<image src="../../static/logo.png" mode="widthFix" class="logo"></image>
		<text class="title">ASWZ网络之家</text>
		<button class="loginBtn" @click="getUserInfo">一键登录</button>
	</view>
</template>

<script>
	import {
		baseUrl
	} from '../../util/config.js'
	export default {
		data() {
			return {
				code: "",
				openid:""
			}
		},
		onLoad() {
			uni.login({
				success: (res) => {
					if (res.errMsg == "login:ok") {
						this.code = res.code;
						console.log(res)
						uni.request({
							url:baseUrl+'/newapi/api/WechatUser/getopenid',
							data:{
								id:res.code
							},
							success:(ress)=>{
								this.openid=ress.data.data;
								uni.setStorageSync('openid',ress.data.data)
							}
						})
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
				uni.getUserProfile({
					desc: "aswz网络之家获取您的微信信息",
					success:(res)=>{
						uni.setStorageSync("userInfo",res.userInfo);
						uni.request({
							url:baseUrl+'/newapi/api/WechatUser/gettoken',
							method:'POST',
							data:{
								...res.userInfo,
								gender:String(res.userInfo.gender),
								js_code:this.code,
								openid:this.openid
							},
							success(r) {
								uni.setStorageSync('token',r.data.data)
							}
						})
						uni.redirectTo({
							url:"../register/register"
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

	.loginBtn {
		width: 80%;
		color: #FFFFFF;
		background: #44652e;
		margin-top: 100rpx;
	}
</style>
