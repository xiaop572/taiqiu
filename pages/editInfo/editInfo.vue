<template>
	<view>
		<u-upload max-count="1" upload-text="上传照片" ref="uUpload" :action="action" on-success="uploadSuccess"></u-upload>
		<u-input v-model="value" :type="type" :border="border" />
		<u-input v-model="value" :type="type" :border="border" />
		<u-input v-model="value" type="textarea" :border="border" />
		<button class="submit" @click="submit">修改</button>
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
					mobile: '',
					captcha: '',
					value: '',
					type: 'text',
					border: true
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
				console.log(files)
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
