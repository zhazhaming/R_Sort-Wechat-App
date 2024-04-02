
<template>
  <div class="activity-modules" :style="{ backgroundImage: 'url(' + 'https://ice.frostsky.com/2024/03/02/09c760c10a7ac7340a09ea8b2f6ada5c.jpeg' + ')' }">
    <div v-for="(activity,index) in services" :key="activity.id" @click="viewService(activity)" class="module">
      <img :src="image[index]"  class="activity-image"/>
      <div class="activity-info">
        <h2>{{ activity.subject }}</h2>
        <p>发布者: {{ activity.districtName }}</p>
        <p>地点: {{ activity.missionRegionName }}</p>
        <p>开始时间: {{ activity.startDate }}</p>
        <p>结束时间: {{ activity.endDate }}</p>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from 'axios';

export default {
  data() {
    return {
      services: [],
	  image:[],
    };
  },
  mounted() {
    this.fetchServices();
  },
  methods: {
    fetchServices() {
      // 发起请求获取志愿服务数据
      uni.request({
      	// url: 'http://192.168.47.48:8009/api/v1/volunteer/getVolunteerList?pageNum=1&pageSize=5',
      	url: 'http://localhost:8009/api/v1/volunteer/getVolunteerList?pageNum=1&pageSize=10',
      	success: (res) => {
      		console.log(res)
      		console.log(res.data)
      		this.services = res.data.data;
      	}
      });
	  uni.request({
	  	url: 'http://localhost:8009/api/v1/images/random?pageSize=10',
	  	success:(res) =>{
	  			  console.log(res.data)
	  			  this.image = res.data.data;
	  	},
		
	  });
    },
    viewService(service) {
      // 点击服务后的操作，例如跳转到详情页
	  const imgUrl = service.url
	  console.log('View url:', imgUrl);
	  wx.navigateTo({
		  url: `./out1/out1?url=${encodeURIComponent(imgUrl)}`
	  })
    }
  }
};
</script>

<style scoped>
	
.activity-modules{
	width: 100%;
	  height: 100%;
	  background-size: cover; /* 背景图片覆盖整个容器 */
	  background-position: center; /* 背景图片居中 */
}
.module {
  margin: 10px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
}
.activity-image {
	width: 100%; /* 图片宽度充满模块宽度 */
    height: auto; /* 图片高度自动调整以保持纵横比 */
    aspect-ratio: 16 / 9; /* 您想要的长方形图片比例，这里是16:9 */
    object-fit: cover; /* 图片覆盖元素的整个内容区域 */
}
.activity-info {
  margin-top: 10px;
}
</style>
