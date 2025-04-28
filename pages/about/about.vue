<template>
  <view class="about">
    <canvas canvas-id="bubble" :style="'width:' + width + 'px;height:' + height + 'px'" class="like-fx"></canvas>
    <like-fx ref="likeFx" :width="width" :height="height"></like-fx>
    <view class="titleZ text-center align-center">
      <text style="font-size: 34rpx;" class="text-center">Hello!你好吖\n欢迎使用「电气试验宝典」小程序\n点击右上角「添加到我的小程序」，\n可以更快捷的找到我哦！</text>
      <text style="font-size: 34rpx;">\n\n本项目成立于2024年11月\n初衷是为广大电气试验人员提供便利\n本小程序所得一切数据不代表完全适用\n本小程序不能作为试验判断的唯一依据\n请遵循相关标准，请结合实际情况使用\n如发现任何问题或错误请及时联系作者\n如有建议和意见欢迎指出\n项目作者：张欢\n\n</text>
      <view class="bt">
        <button class="btn" open-type="contact">联系客服</button>
        <button class="btn" open-type="feedback">官方反馈</button>
        <button class="btn" @click="showRewardAd">支持作者</button>
      </view>
    </view>
  </view>
</template>

<script>
import LikeFx from '@/diyzj/linke.vue';
export default {
  components: {
    LikeFx
  },
  data() {
    return {
      animation_timer: null, 
      width: 375,
      height: 1920,
      videoAd: null
    };
  },
  onLoad() {
    this._startLikeAnimation();
    if (uni.createRewardedVideoAd) {
      this.videoAd = uni.createRewardedVideoAd({
        adUnitId: 'adunit-46ea256f62108ab8'
      });
      this.videoAd.onLoad(() => {});
      this.videoAd.onError((err) => {
        console.error('激励视频广告加载失败', err);
      });
      this.videoAd.onClose((res) => {});
    }
  },
  onUnload() {
    clearInterval(this.animation_timer);
  },
  methods: {
    _startLikeAnimation() {
      this.animation_timer = setInterval(() => {
        this.$refs.likeFx.likeClick();
      }, 300);
    },
    showRewardAd() {
      if (this.videoAd) {
        this.videoAd.show().catch(() => {
          this.videoAd.load()
            .then(() => this.videoAd.show())
            .catch((err) => {
              console.error('激励视频广告显示失败', err);
            });
        });
      }
    }
  }
};
</script>

<style scoped>
.titleZ {
  width: 750rpx;
  font-size: 52rpx;
  margin-top: 10rpx;
}
.contentZ {
  width: 650rpx;
  margin: 10rpx auto 0;
  text-align: left;
}
.about-bg {
  background-size: cover;
  width: 100vw;
  height: 100vh;
  justify-content: center;
  flex-direction: column;
  color: #fff;
}

.edit-fixed {
  position: fixed;
  width: 100%;
  bottom: 0;
  z-index: 1024;
  box-shadow: 0 1rpx 6rpx rgba(0, 0, 0, 0.1);
}

.detail-imgs image {
  width: 100%;
  float: left;
  border: 0;
  padding: 0;
  margin: 0;
}

.share-img {
  position: fixed;
  padding: 10rpx;
  width: 100rpx;
  height: 100rpx;
  bottom: 200rpx;
  right: 20rpx;
  z-index: 1024;
  opacity: 0.8;
  box-shadow: 0rpx 8rpx 30rpx 0rpx rgba(0, 0, 0, 0.3);
  border: none;
}

.about {
  margin: 0;
  width: 100%;
  height: 100vh;
  padding-top: 20%;
  color: #fff;
  background: linear-gradient(-120deg, #F15BB5, #9A5CE5, #01BEFF, #00F5D4);
  background-size: 500% 500%;
  animation: gradientBG 15s ease infinite;
}

@keyframes gradientBG {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.container {
  width: 100%;
  position: absolute;
  text-align: center;
}

.like-fx {
  position: fixed;
  right: 0;
  z-index: 1024;
  pointer-events: none;
}
.bt {
  display: flex;
}
.btn {
  margin-top: 10rpx;
  background: linear-gradient(to bottom, #6180ee, #4c8ef2);
  height: 80rpx;
  width: 320rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 30rpx;
  margin-left: 10rpx;
}
.btn:active {
  transform: scale(0.96);
  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
}
</style>    