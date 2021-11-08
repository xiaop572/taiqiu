<template>
	<view>
		<hans-tabber :list="lists" :currents="currents" style="position:fixed;bottom:0;width:100%;left:0;right:0;" @tabChange="tabChange">
		</hans-tabber>
	</view>
</template>

<script>
	import hansTabber from '../hans-tabbar/hans-tabbar.vue'
	import tabbar from '../../util/tabbarConfig.js'
	export default {
		components: {
			hansTabber
		},
		data() {
			return{
				lists:[],
				index:0,
				currents:0
			}
		},
		methods: {
			tabChange(index) {
				uni.navigateTo({
					url:this.lists[index].pagePath
				})
			}
		},
		mounted() {
			let state=false;
			this.lists=tabbar.list;
			const pages=getCurrentPages();
			const path=pages[pages.length-1].$page.fullPath;
			this.lists.forEach((item,index)=>{
				if(path.indexOf(item.pagePath)>=0){
					this.currents=index;
					state=true;
				}
			})
			if(!state){
				this.currents=-1
			}
		}
	}
</script>

<style>
</style>
