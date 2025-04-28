<template>
    <view>
        <view class="tips-box" v-if="showTip">
            <view class="tips-content" @tap="hideTip">
                <view class="tips-arrow"></view>
                <text class="tips-text">{{ tip }}</text>
            </view>
        </view>
    </view>
</template>

<script>
	const SHOW_TIP = "SHOW_TIP";
export default {
    data() {
        return {
            showTip: false,
            timer: null,
            customBarHeight: 0
        };
    },
    mounted() {
        // 使用新的 API 获取系统信息
        const windowInfo = uni.getWindowInfo();
        const deviceInfo = uni.getDeviceInfo();
        const appBaseInfo = uni.getAppBaseInfo();
        const systemSetting = uni.getSystemSetting();
        this.customBarHeight = windowInfo.statusBarHeight + 44; // 44是默认导航栏高度
        
        // 检查本地存储中是否已经显示过提示
        try {
            const storageInfo = uni.getStorageInfoSync();
            this.showTip = !storageInfo.keys.includes(SHOW_TIP);
        } catch (e) {
            console.error('获取存储信息失败:', e);
            this.showTip = true;
        }

        // 设置定时器，自动隐藏提示
        const validDuration = typeof this.duration === 'number' ? this.duration : 5;
        this.timer = setTimeout(() => {
            this.showTip = false;
        }, validDuration * 1000);
    },
    beforeDestroy() {
        // 清理定时器
        if (this.timer) {
            clearTimeout(this.timer);
            this.timer = null;
        }
    },
    props: {
        tip: {
            type: String,
            default: "点击「添加小程序」，下次访问更便捷"
        },
        duration: {
            type: Number,
            default: 5,
            required: false
        }
    },
    methods: {
        hideTip() {
            try {
                uni.setStorageSync(SHOW_TIP, true);
                this.showTip = false;
            } catch (e) {
                console.error('设置存储失败:', e);
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.tips-box {
  position: fixed;
  /* 使用 JS 计算的 customBarHeight */
  top: v-bind(customBarHeight + 'px');
  right: -20rpx;
  z-index: 99999;
  opacity: 0.8;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  flex-direction: column;
  width: 600rpx;
  animation: tips-animation 1s linear infinite;
}

.tips-content {
  border-width: 0;
  margin-top: 20rpx;
  position: relative;
  background-color: #34b5e2;
  box-shadow: 0 10rpx 20rpx -10rpx #34b5e2;
  border-radius: 12rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 18rpx 20rpx;
  margin-right: 40rpx;
}

.tips-arrow {
  position: absolute;
  width: 0;
  height: 0;
  top: -38rpx;
  right: 105rpx;
  border: 20rpx solid transparent;
  border-bottom-color: #34b5e2;
}

.tips-text {
  color: #fff;
  font-size: 28rpx;
  font-weight: 400;
}

@keyframes tips-animation {
  0% { 
    opacity: 0.8; 
  }
  50% { 
    opacity: 1; 
  }
}
</style>
