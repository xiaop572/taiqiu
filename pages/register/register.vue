<template>
	<view class="register">
		<u-upload max-count="1" upload-text="上传照片" ref="uUpload" :action="action" on-success="uploadSuccess"></u-upload>
		<view class="Input">
			<u-input v-model="form.realname" :type="type" :border="border" placeholder="真实姓名" />
		</view>
		<view class="Input">
			<u-input v-model="form.cardno" :type="type" :border="border" placeholder="身份证号" />
		</view>
		<button class="submit" @click="submit">注册</button>
	</view>
</template>

<script>
	import {
		baseUrl
	} from '../../util/config.js'
	export default {
		data() {
			return {
				form: {
					realname: '',
					cardno: ''
				},
				action: baseUrl + '/newapi/api/user/uploadimg',
				border: "1px solid #ccc"
			}
		},
		methods: {
			uploadSuccess(data) {
				console.log(data, "上传成功")
			},
			submit() {
				let files = [];
				files = this.$refs.uUpload.lists.filter(val => {
					return val.progress == 100;
				})
				const filesArr = files[0].response.Data.list;
				if (!this.form.realname || !this.form.cardno) {
					uni.showToast({
						title: '信息填写不完整',
						duration: 2000
					});
				}
				if (!filesArr || filesArr.length <= 0) {
					uni.showToast({
						title: '请上传照片',
						duration: 2000
					});
				}
				uni.request({
					url: baseUrl + '/newapi/api/WechatUser/setuserinfo',
					method:"POST",
					data: {
						openid:uni.getStorageSync('openid'),
						realname:this.form.realname,
						cardno:this.form.cardno,
						mobile:"",
						memo:""
					}
				})
				uni.request({
					url: baseUrl + '/newapi/api/WechatUser/setphoto',
					method:"POST",
					data: {
						openid:uni.getStorageSync('openid'),
						photo1:filesArr[0].file_path
					}
				})
				// uni.navigateTo({
				// 	url:"../home/home"
				// })
			}
		}
	}
</script>

<style lang="less">
	.u-upload {
		justify-content: center;
	}

	.Input {
		width: 600rpx;
		margin: 40rpx auto 0 auto;
	}

	.submit {
		background: #44652e;
		width: 80%;
		color: #FFFFFF;
		background: #44652e;
		margin-top: 100rpx;
	}
</style>
