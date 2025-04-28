<template>
  <view class="container">
    <!-- 在线预览区域 -->
    <web-view 
      :src="previewUrl" 
      @message="handleMessage" 
      @error="handleError"
      @loaded="onWebViewLoaded">
      <!-- 可选：在 web-view 加载时显示加载指示器 -->
      <view class="loading" v-if="loading">
        <text>加载中...</text>
      </view>
    </web-view>
  </view>
</template>

<script>
	import { shareMixin } from '/shareMixin.js';    //分享小程序的js引入
export default {
  mixins: [shareMixin],  //分享小程序的js引入
  data() {
    return {
	  shareTitle: '电气试验宝典-在线预览',     // 设置自定义的分享标题
      previewUrl: '', // 预览的URL
      loading: true // 控制加载指示器的显示
    };
  },
  onLoad(options) {
    if (options && options.url) {
      // 解码URL参数
      this.previewUrl = decodeURIComponent(options.url);
      console.log('预览的URL:', this.previewUrl);
    } else {
      // 如果没有传递URL参数，显示错误提示
      uni.showToast({
        title: '无效的预览链接。',
        icon: 'none',
        duration: 3000
      });
      // 可选：延迟后关闭当前页面
      setTimeout(() => {
        uni.navigateBack();
      }, 3000);
    }
  },
  methods: {
    /**
     * 处理来自 web-view 的消息
     */
    handleMessage(event) {
      console.log('来自 web-view 的消息:', event.detail.data);
      // 这里可以处理来自网页的消息，例如下载事件等
      // 例如，如果网页发送了一个下载请求，可以在这里处理
    },

    /**
     * 处理 web-view 加载错误
     */
    handleError(event) {
      console.error('web-view 加载错误:', event.detail.errMsg);
      this.loading = false; // 隐藏加载指示器
      uni.showToast({
        title: '预览失败，请重试。',
        icon: 'none',
        duration: 3000
      });
      // 可选：延迟后关闭当前页面
      setTimeout(() => {
        uni.navigateBack();
      }, 3000);
    },

    /**
     * 处理 web-view 加载完成事件
     */
    onWebViewLoaded() {
      this.loading = false; // 隐藏加载指示器
      console.log('web-view 加载完成');
    }
  }
};
</script>

<style scoped>
/* 容器样式 */
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

/* web-view 样式 */
web-view {
  flex: 1;
  width: 100%;
}

/* 加载指示器样式 */
.loading {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 24rpx;
  color: #888;
  z-index: 999;
}
</style>