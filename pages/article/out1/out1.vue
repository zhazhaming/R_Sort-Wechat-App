<template>
	<view>
		<!-- https://www.izyz.org/mission/detail-7959231 -->
		<web-view :src=imgurl></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imgurl: "",
			}
		},
		methods: {
			onLoad(options) {
			    const url = decodeURIComponent(options.url);
			    // 在此处根据传递的 url 参数进行相应操作
				this.imgurl = url;
				console.log(this.imgurl)
			  }
		}
	}
</script>

<style>

</style>
