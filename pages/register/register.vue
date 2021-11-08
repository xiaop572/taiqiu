<template>
	<view class="register">
		<u-upload max-count="1" upload-text="上传照片" ref="uUpload" :before-upload="upload"></u-upload>
		<view class="Input">
			<u-input v-model="value" :type="type" :border="border" placeholder="真实姓名"/>
		</view>
		<view class="Input">
			<u-input v-model="value" :type="type" :border="border" placeholder="身份证号"/>
		</view>
		<button class="submit" @click="submit">注册</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				form: {
					mobile: '',
					captcha: ''
				},
				border:"1px solid #ccc"
			}
		},
		methods: {
			upload() {
				console.log(this.$refs.uUpload.lists)
			},
			submit(){
				uni.navigateTo({
					url:"../home/home"
				})
			}
		}
	}
</script>

<style lang="less">

	.u-upload {
		justify-content: center;
	}
	.Input{
		width: 600rpx;
		margin:40rpx auto 0 auto;
	}
	.submit{
		background: #44652e;
		width: 80%;
		color: #FFFFFF;
		background: #44652e;
		margin-top: 100rpx;
	}
</style>
