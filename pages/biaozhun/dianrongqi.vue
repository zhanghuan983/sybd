<template>
  <view class="container">
    <!-- 顶部 Tab 按钮 -->
    <view class="tab-bar">
      <view class="tab-item" :class="{ active: activeTab === 'tab1' }" @click="switchTab('tab1')">
        预防性试验
      </view>
      <view class="tab-item" :class="{ active: activeTab === 'tab2' }" @click="switchTab('tab2')">
        交接性试验
      </view>
      <!-- 底部滑动条 -->
      <view class="tab-indicator" :style="{ left: indicatorLeft }"></view>
    </view>

    <!-- Tab1 内容区域 -->
    <view class="tab-content">
      <view v-if="activeTab === 'tab1'" class="tab-pane" :style="{ transform: 'translateX(' + (activeTab === 'tab1' ? '0' : '100%') + ')' }">
	  <!-- 滚动通知 -->
	  <uv-notice-bar :text="listtxt1" mode="closable" bgColor="#fef0f0" color="#e45656"></uv-notice-bar>
	  <view class="txtdown"> DL/T 596-2021 标准文件：
		<view class="copy-link" @click="previewOnline" style="width: 140rpx;">在线预览</view>
		<view class="copy-link" @click="copyText">文件下载</view>
	  </view>
	 <!-- 页面内容 -->
	         <view class="list-title">14、电容器</view>
	         <!-- 列表项 -->
	         <view class="list">
	           <block v-for="(item, index) in listItems" :key="index">
	             <view class="list-item" @click="navigateTo(item.url)">
	               <!-- 列表项的文字 -->
	               <text class="item-text">{{ item.text }}</text>
	               <!-- 列表项的图片 -->
	               <image class="item-image" src="/static/you.png" mode="aspectFit"></image>
	             </view>
	             <!-- 列表项之间的灰色实线 -->
	             <view class="divider"></view>
	           </block>
	         </view>
	    </view>
      
	  
	  <view v-if="activeTab === 'tab2'" class="tab-pane" :style="{ transform: 'translateX(' + (activeTab === 'tab2' ? '0' : '100%') + ')' }">
      <!-- 滚动通知 -->
      <uv-notice-bar :text="listtxt2" mode="closable" bgColor="#fef0f0" color="#e45656"></uv-notice-bar>
      <view class="txtdown"> GB 50150-2016 标准文件：
      		<view class="copy-link" @click="previewOnline2" style="width: 140rpx;">在线预览</view>
      		<view class="copy-link" @click="copyText2">文件下载</view>
      </view>
		
		<view class="list-title">14、电容器</view>
		<!-- 列表项 -->
		<view class="list">
		  <block v-for="(item, index) in listItems" :key="index">
		    <view class="list-item" @click="navigateTo(item.url)">
		      <!-- 列表项的文字 -->
		      <text class="item-text">{{ item.text }}</text>
		      <!-- 列表项的图片 -->
		      <image class="item-image" src="/static/you.png" mode="aspectFit"></image>
		    </view>
		    <!-- 列表项之间的灰色实线 -->
		    <view class="divider"></view>
		  </block>
		</view>
		
	  </view>
    </view>
  </view>
</template>

<script>
	import { shareMixin } from '/shareMixin.js';    //分享小程序的js引入

export default {
  mixins: [shareMixin],  //分享小程序的js引入
  data() {
    return {
	  description: '',
	  title: '',
	  listtxt1:'依据：《电力设备预防性试验规程 DL/T 596-2021》，页面勘误请联系QQ/WX：453555098',
	  listtxt2:'依据：《电气装置安装工程电气设备交接试验标准 GB 50150-2016》，页面勘误请联系QQ/WX：453555098',
	  activeTab: 'tab1', // 当前激活的 Tab
      indicatorLeft: '0px', // 滑动条的位置
	  linkToCopy: 'https://p.huanvip.cn/down.php/45742b8363224b74ff4f65db098659e8.pdf',
	  previewLink: 'https://mp.weixin.qq.com/s/Erf53RndAz_OL4hd9MLceA',
	  linkToCopy2:'https://p.huanvip.cn/down.php/8fd7893e0496a9fe799a2e27d658eef0.pdf',
	  previewLink2:'https://mp.weixin.qq.com/s/RtZzklxaYYttVIdipUywUg',
	  listItems: [
	          { text: '14.1 高压并联电容器、串联电容器和交流滤波电容器', url: '/pages/preview/preview?url=https://mp.weixin.qq.com/s/VFPqTD4ZD298RE4V0ekokw' },      //  { text: '5.1 同步发电机和调相机', url: '/pages/biaozhun/diandongji51' },
	          { text: '14.2 断路器电容器', url: '/pages/preview/preview?url=https://mp.weixin.qq.com/s/1jByG3mc27CCBvIsr5qv6g' },
			  { text: '14.3 集合式电容器、箱式电容器', url: '/pages/preview/preview?url=https://mp.weixin.qq.com/s/fC9KY2i1ln5S9KBbT2eKpQ' },
			  
			  // 你可以根据需要添加更多列表项
	        ],
	  }
  },
  computed: {
  	
  },
  
  computed: {

  	},
  
  methods: {
	switchTab(tab) {
	  if (this.activeTab === tab) return;
	  
	  this.activeTab = tab;
	  
	  // 计算滑动条的新位置
	  if (tab === 'tab1') {
	    this.indicatorLeft = '0%'; // 指示条在 tab1 时位于左侧
	  } else if (tab === 'tab2') {
	    this.indicatorLeft = '50%'; // 指示条在 tab2 时位于屏幕中间
	  }
	},
	//  复制文件下载地址
	copyText() {
	  const text = this.linkToCopy;
	  // 使用 uni.setClipboardData API 复制文本到剪贴板
	  uni.setClipboardData({
	    data: text,
	    success: () => {
	      // 复制成功后，显示提示信息
	      uni.showToast({
	        title: '链接已复制,打开浏览器下载',
	        icon: 'success', // 图标类型：'success' | 'loading' | 'none'
	        duration: 2000 // 提示显示时间，单位为毫秒
	      });
	    },
	    fail: () => {
	      // 复制失败时，显示错误提示
	      uni.showToast({
	        title: '复制失败，请重试。',
	        icon: 'none',
	        duration: 3000
	      });
	    }
	  });
	},
	//  在线预览
	// 主页面方法
	previewOnline() {
	  uni.navigateTo({
	    url: '/pages/preview/preview?url=' + encodeURIComponent(this.previewLink),
	    success: () => {
	      console.log('在线预览页面跳转成功');
	    },
	    fail: () => {
	      uni.showToast({
	        title: '在线预览失败，请重试。',
	        icon: 'none',
	        duration: 3000
	      });
	    }
	  });
	},
	copyText2() {
	  const text2 = this.linkToCopy2;
	  // 使用 uni.setClipboardData API 复制文本到剪贴板
	  uni.setClipboardData({
	    data: text2,
	    success: () => {
	      // 复制成功后，显示提示信息
	      uni.showToast({
	        title: '链接已复制,打开浏览器下载',
	        icon: 'success', // 图标类型：'success' | 'loading' | 'none'
	        duration: 2000 // 提示显示时间，单位为毫秒
	      });
	    },
	    fail: () => {
	      // 复制失败时，显示错误提示
	      uni.showToast({
	        title: '复制失败，请重试。',
	        icon: 'none',
	        duration: 3000
	      });
	    }
	  });
	},
	//  在线预览
	// 主页面方法
	previewOnline2() {
	  uni.navigateTo({
	    url: '/pages/preview/preview?url=' + encodeURIComponent(this.previewLink2),
	    success: () => {
	      console.log('在线预览页面跳转成功');
	    },
	    fail: () => {
	      uni.showToast({
	        title: '在线预览失败，请重试。',
	        icon: 'none',
	        duration: 3000
	      });
	    }
	  });
	},
	
  	// 在原 export default 的对象内部的 methods 中添加或修改以下 navigateTo 方法
	navigateTo(url) {
	    // 使用 uni-app 的导航 API uni.navigateTo 进行页面跳转
	    uni.navigateTo({
	        url: url
	    });
	},
}
}

</script>

<style scoped>
/* 容器样式 */
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

/* Tab 栏样式 */
.tab-bar {
  position: relative;
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 80rpx;
  background-color: #ffffff;
  border-bottom: 2rpx solid #e0e0e0;
}

/* Tab 按钮样式 */
.tab-item {
  position: relative;
  flex: 1; /* 每个 Tab 按钮占据屏幕的一半 */
  height: 100%;
  line-height: 80rpx;
  text-align: center;
  font-size: 34rpx;
  color: #666666;
  cursor: pointer;
}

/* 激活状态的 Tab 按钮样式 */
.tab-item.active {
  color: #007aff;
}

/* 滑动指示条样式 */
.tab-indicator {
  position: absolute;
  bottom: 0;
  height: 4rpx;
  width: 50%; /* 指示条宽度为屏幕的一半 */
  background-color: #007aff;
  transition: left 0.3s ease;
}

/* Tab 内容区域样式 */
.tab-content {
  display: flex;
  flex: 1;
  position: relative;
  width: 100%;
  overflow: visible; 
}

/* 每个 Tab 面板的样式 */
.tab-pane {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transition: transform 0.3s ease;
  background-color: #f9f9f9;
  overflow: visible;
}
.txtdown{
	height: 78rpx;
	width: 750rpx;
	background-color: #fef0f0;
	display: flex;
	float: left;
	align-items: center;
	padding: 14rpx;
	font-size: 30rpx;
	color: #ec8585;
	margin-top: 3rpx;
	margin-bottom: 30rpx;
}
.txtdown2{
	height: 78rpx;
	width: 750rpx;
	background-color: #fdf6ec;
	display: flex;
	float: left;
	align-items: center;
	padding: 14rpx;
	font-size: 30rpx;
	color: #f9ae3d;
	margin-top: 3rpx;
	margin-bottom: 5rpx;
}
.copy-link {
  color: #3c9cff; /* 超链接颜色 */
  text-decoration: underline; /* 下划线 */
  cursor: pointer; /* 鼠标悬停时显示手型 */
  font-size: 28rpx;
}
.list-title {
  font-size: 40rpx;
  font-weight: bold;
  padding-left: 10rpx;
  padding-bottom: 10rpx;
}

.list {
  background-color: #ebfeff;
}

.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30rpx 20rpx;
   
  
}

.divider {
  height: 1px;
  background-color: #d3d3d3;
}

.item-text {
  font-size: 30rpx;
  color: #333333;
}

.item-image {
  width: 38rpx;
  height: 38rpx;
}


			
		
	
</style>
