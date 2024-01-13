<template>
	<view>
		<view class="background">
			<view>
				<image class="article" src="https://s2.loli.net/2022/06/15/l7nwdC5kMRtK3fr.png" @click="toarticle"></image>
				<image class="participate" src="https://s2.loli.net/2022/06/15/vtF6Nrcz7aifHLD.png" @click="toparticipate"></image>
				<image class="competition" src="https://s2.loli.net/2022/06/15/BeUgLxirXyadMcl.png" @click="tocompetition"></image>
				<!-- <image class="game" src="https://636c-cloud1-5gy3mgvy401e933b-1306354275.tcb.qcloud.la/game.png?sign=7a8d8a3793d6be8093d343731f74b01c&t=1644754338"></image> -->
			</view>
		</view>
		<view class="video">
			<video class="video1"
				src="https://vd4.bdstatic.com/mda-kibtiafebga3g39k/v1-cae/sc/mda-kibtiafebga3g39k.mp4?v_from_s=hkapp-haokan-hna&auth_key=1656145640-0-0-859792f278794c4ebdf2abb1389817a6&bcevod_channel=searchbox_feed&pd=1&cd=0&pt=3&logid=3440302636&vid=2013854237229207438&abtest=102777_5-102784_1-102836_3-102976_1-17451_2-3000232_1&klogid=3440302636"></video>
			<video class="video2"
				src="https://vd3.bdstatic.com/mda-khdu537a1ieh5s8j/hd/mda-khdu537a1ieh5s8j.mp4?v_from_s=hkapp-haokan-hnb&auth_key=1656144774-0-0-01e191a05854f2eb54bcc35dcdac2e84&bcevod_channel=searchbox_feed&pd=1&cd=0&pt=3&logid=2574043710&vid=6492077294297376241&abtest=102777_5-102784_1-102836_3-102976_1-17451_2-3000232_1&klogid=2574043710"></video>
			<video class="video3"
				src="https://vd4.bdstatic.com/mda-iiicwu82yrs5w5kk/sc/mda-iiicwu82yrs5w5kk.mp4?v_from_s=hkapp-haokan-hna&auth_key=1656144935-0-0-7c8efc88f8df32f29609bd0cedf4eb84&bcevod_channel=searchbox_feed&pd=1&cd=0&pt=3&logid=2735241313&vid=11628475743862028112&abtest=102777_5-102784_1-102836_3-102976_1-17451_2-3000232_1&klogid=2735241313"></video>
			<video class="video4"
				src="https://vd2.bdstatic.com/mda-kf00cg5ucva4r157/sc/mda-kf00cg5ucva4r157.mp4?v_from_s=hkapp-haokan-hnb&auth_key=1656144053-0-0-925d85f422e4797ebb7d71eb5f5796df&bcevod_channel=searchbox_feed&pd=1&cd=0&pt=3&logid=1853197543&vid=4656496370393887600&abtest=102777_5-102784_1-102836_3-102976_1-17451_2-3000232_1&klogid=1853197543"></video>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {
			toparticipate() {
				wx.navigateTo({
					url: '../participate/participate'
				})
			},
			toarticle() {
				wx.navigateTo({
					url: '../article/article'
				})
			},
			tocompetition() {
				wx.navigateTo({
					url: '../competition/competition'
				})
			},
		}
	}
</script>

<style scoped>
	.background {
		width: 100%;
		height: 500px;
		background-image: url(https://s2.loli.net/2022/06/15/Fzk72QUNxAsiIao.png);
		background-size: 100% 100%;
		position: relative;
	}

	.participate {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		left: 20%
	}

	.article {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		left: 45%;
	}

	.competition {
		width: 50px;
		height: 64.5px;
		position: absolute;
		top: 350px;
		right: 20%;
	}

	.game {
		width: 46px;
		height: 60.5px;
		position: absolute;
		top: 350px;
		right: 35%;
	}

	.video {
		width: 100%;
		height: 200px;
		background-image: url(https://s2.loli.net/2022/06/15/wKFABZT7u86O4cG.png);
		background-size: 100% 100%;
		position: relative;
		margin-top: -50px;
	}

	.video1 {
		position: absolute;
		top: 50px;
		left: 20px;
		width: 170px;
		height: 100px;
	}

	.video2 {
		position: absolute;
		top: 50px;
		right: 20px;
		width: 170px;
		height: 100px;
	}

	.video3 {
		position: absolute;
		top: 200px;
		left: 20px;
		width: 170px;
		height: 100px;
	}

	.video4 {
		position: absolute;
		top: 200px;
		right: 20px;
		width: 170px;
		height: 100px;
	}
</style>
