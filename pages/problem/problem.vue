<template>
	<view>
		<u-collapse>
			<u-collapse-item :title="item.head" v-for="(item, index) in itemList" :key="index">
				{{item.body}}
			</u-collapse-item>
		</u-collapse>
		<tab-bar></tab-bar>
	</view>
</template>

<script>
	import tabBar from '../../components/tabbar/tabbar.vue'
	import {
		baseUrl
	} from '../../util/config.js'
	export default {
		components: {
			tabBar
		},
		data() {
			return {
				itemList: []
			}
		},
		mounted() {
			uni.request({
				url: baseUrl + '/newapi/api/faq/getallfaq',
				data: {
					curpage:1,
					limit:9999
				},
				success: () => {
					
				}
			})
		}
	}
</script>

<style>
</style>
