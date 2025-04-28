<template>
    <view >
        <add-tip :tip="tip" :duration="duration" />
        <uv-swiper :list="listswi" height="280rpx" indicator previousMargin="30" 
        nextMargin="30" circular :autoplay="true" radius="5" bgColor="#ffffff" interval="3000"></uv-swiper>
        <uv-notice-bar :text="listtxt" mode="closable" style="border-radius: 20rpx;margin: 15rpx 10rpx -5rpx 10rpx;" linkType="contact"></uv-notice-bar>
        <view class="wrap " >
            <view class="nav_title ">在 线 计 算 工 具</view>
        </view>


        <scroll-view scroll-y class="page">
            <view class="nav-list">
                <navigator hover-class="none" :url="'/pages/tool/' + item.name1" class="nav-li" navigateTo :class="'bg-'+item.color"
                 :style="[{animation: 'show ' + ((index+1)*0.2+1) + 's 1'}]" v-for="(item,index) in elements" :key="index">
                    <view class="nav-title">{{item.title}}</view>
                    <view class="nav-name">{{item.name}}</view>
                    <text :class="'cuIcon-' + item.cuIcon"></text>
                </navigator>
            </view>
        </scroll-view>
        <view class="wrap2" >
            <view class="nav_title ">相  关  试  验  标  准</view>
        </view>

        <scroll-view scroll-y class="page2">
            <view class="nav-list">
                <navigator hover-class="none" :url="'/pages/biaozhun/' + item.name1" class="nav-li2" navigateTo :class="'bg-'+item.color"
                 :style="[{animation: 'show ' + ((index+1)*0.2+1) + 's 1'}]" v-for="(item,index) in elem" :key="index">
                    <view class="nav-title">{{item.title}}</view>
                    <view class="nav-name">{{item.name}}</view>
                <!-- <text :class="'cuIcon-' + item.cuIcon"></text>    图标-->
                </navigator>
            </view>
        </scroll-view> 	
        <uni-fab
            ref="fab" 
            :pattern="pattern" 
            :content="content" 
            :horizontal="horizontal" 
            :vertical="vertical"
            :direction="direction" 
            @trigger="trigger" 
            @fabClick="fabClick" 
          />
    </view>
</template>

<script>
import { shareMixin } from '/shareMixin.js';    //分享小程序的js引入
import addTip from '/diyzj/tip.vue';            //提示添加小程序
export default {
    mixins: [shareMixin],  //分享小程序的js引入
    components: {
        addTip
    },
    data() {
        return {
            shareTitle: '电气试验宝典-首页', // 设置自定义的分享标题
            tip: '点击「添加小程序」，下次访问更便捷',
            elements: [{
                    title: '电动机直阻计算',
                    name: 'Motor',
                    name1:'diandongji',
                    color: 'cyan',
                },
                {
                    title: '变压器直阻计算',
                    name: 'Transformer',
                    name1:'bianyaqi',
                    color: 'blue',
                },
                {
                    title: '串谐选型工具',
                    name: 'Series resonance',
                    name1:'chuanxie',
                    color: 'purple',
                },
                {
                    title: '温度换算工具 ',
                    name: 'temp',
                    name1:'wendu',
                    color: 'mauve',
                },
                {
                    title: '试验数据初值差 ',
                    name: 'Data Diff',
                    name1:'datadiff',
                    color: 'green',
                },
                {
                    title: '色谱分析三比值法 ',
                    name: 'colour spectrum',
                    name1:'colourspe',
                    color: 'orange',
                },

            ],
            elem: [
                {
                    title: '电动机、发电机',
                    // name: 'Motor',
                    name1:'diandongji',
                    color: 'cyan',
                },
                {
                    title: '变压器',
                    // name: 'Transformer',
                    name1:'bianyaqi',
                    color: 'blue',
                },
                {
                    title: '电抗器及消弧线圈',
                    // name: 'Reactor',
                    name1:'diankangqi',
                    color: 'purple',
                },
                {
                    title: '互感器',
                    // name: 'Transformer',
                    name1:'huganqi',
                    color: 'mauve',
                },
                {
                    title: '开关设备',
                    // name: 'Switch',
                    name1:'kaiguan',
                    color: 'blue',
                },
                {
                    title: '有载调压装置',
                    // name: 'Voltage',
                    name1:'youzai',
                    color: 'purple',
                },
                {
                    title: '套管',
                    // name: 'Switch',
                    name1:'taoguan',
                    color: 'brown',
                },
                {
                    title: '绝缘子',
                    // name: 'Voltage',
                    name1:'jueyuanzi',
                    color: 'yellow',
                },
                {
                    title: '电力电缆线路',
                    // name: 'Switch',
                    name1:'dianlan',
                    color: 'orange',
                },
                {
                    title: '电容器',
                    // name: 'Voltage',
                    name1:'dianrongqi',
                    color: 'cyan',
                },
                {
                    title: '绝缘油和SF6气体',
                    // name: 'Voltage',
                    name1:'yousf',
                    color: 'green',
                },
                {
                    title: '避雷器',
                    // name: 'Switch',
                    name1:'bileiqi',
                    color: 'red',
                },
                {
                    title: '母线',
                    // name: 'Voltage',
                    name1:'muxian',
                    color: 'brown',
                },
                {
                    title: '低压配电装置',
                    // name: 'Transformer',
                    name1:'huganqi',
                    color: 'mauve',
                },
                {
                    title: '架空线路及塔杆',
                    // name: 'Switch',
                    name1:'kaiguan',
                    color: 'blue',
                },
                {
                    title: '接地装置',
                    // name: 'Motor',
                    name1:'diandongji',
                    color: 'cyan',
                },
                {
                    title: '并联电容器装置',
                    // name: 'Transformer',
                    name1:'bianyaqi',
                    color: 'green',
                },
                {
                    title: '串联补偿装置',
                    // name: 'Reactor',
                    name1:'diankangqi',
                    color: 'purple',
                },
                {
                    title: '电除尘器',
                    // name: 'Transformer',
                    name1:'huganqi',
                    color: 'mauve',
                },
                {
                    title: '资料性附录',
                    // name: 'Switch',
                    name1:'kaiguan',
                    color: 'red',
                },
            ],
            listswi: [
                'http://huanvip.cn/pic/1.jpeg',
                'http://huanvip.cn/pic/2.jpeg',
                'http://huanvip.cn/pic/3.jpeg',
                'http://huanvip.cn/pic/4.jpeg',
                'http://huanvip.cn/pic/5.jpeg',
                'http://huanvip.cn/pic/6.jpeg',
                ],
            listtxt:'欢迎使用「试验宝典」，您的鼓励是最大动力，有问题联系作者微信/QQ：453555098！',
            //以下是悬浮按钮的配置
            title: 'uni-fab',
            directionStr: '垂直',
            horizontal: 'right',
            vertical: 'bottom',
            direction: 'horizontal',
            pattern: {
            color: '#7A7E83',
            backgroundColor: '#fff',
            selectedColor: '#007AFF',
            buttonColor: '#007AFF',
            iconColor: '#fff'
            },
            is_color_type: false,
            content: [
              {
                iconPath: '/static/home.png',
                selectedIconPath: '/static/home.png',
                text: '首页',
                active: false
              },
              {
                iconPath: '/static/real.png',
                selectedIconPath: '/static/real.png',
                text: '资源',
                active: false
              },
              {
                iconPath: '/static/account.png',
                selectedIconPath: '/static/account.png',
                text: '关于',
                active: false
              },
              {
                iconPath: '/static/fenxiang.png',
                selectedIconPath: '/static/fenxiang.png',
                text: '分享',
                active: false
              },
              {
                iconPath: '/static/zan.png',
                selectedIconPath: '/static/fenxiang.png',
                text: '赞赏',
                active: false
              }
            ],
            // 以上是悬浮按钮的配置
            videoAd: null
        };
    },
    onLoad() {
        if (uni.createRewardedVideoAd) {
            this.videoAd = uni.createRewardedVideoAd({
                adUnitId: 'adunit-46ea256f62108ab8'
            });
            this.videoAd.onLoad(() => {});
            this.videoAd.onError((err) => {
                console.error('激励视频广告加载失败', err);
            });
            this.videoAd.onClose((res) => {
                if (res && res.isEnded) {
                    // 广告奖励成功获取后的处理逻辑
                    uni.showToast({
                        title: '感谢您的支持！',
                        icon: 'success',
                        duration: 2000
                    });
                } else {
                    uni.showToast({
                        title: '未完整观看广告，无法获得赞赏奖励！',
                        icon: 'none',
                        duration: 3000
                    });
                }
            });
        }
    },
    mounted() {
        // 在页面加载完成后调用uni-fab的open方法展开组件
        this.$refs.fab.open();
        // 设置定时器，8秒后关闭uni-fab
        setTimeout(() => {
            this.$refs.fab.close();
        }, 8000);
    },
    methods: {

        // 以下是处理悬浮按钮的点击事件
        trigger(e) {
            const { index } = e;
            switch (index) {
                case 0:
                    // 跳转到首页
                    uni.navigateTo({
                        url: '/pages/index/index' // 请根据实际情况修改首页路径
                    });
                    break;
                case 1:
                    // 处理资源点击
                    uni.navigateTo({
                        url: '/pages/ziyuan/ziyuan' // 请根据实际情况修改资源路径
                    });
                    break;
                case 2:
                    // 处理关于点击
                    uni.navigateTo({
                        url: '/pages/about/about' // 请根据实际情况修改关于路径
                    });
                    break;
                case 3:
                    uni.showToast({
                        title: '请点击小程序右上角进行分享，感谢您的支持。',
                        icon: 'none'
                    });
                    break;
                case 4:
                    // 点击赞赏按钮，显示激励广告
                    if (this.videoAd) {
                        uni.showToast({
                            title: '观看广告完成赞赏！',
                            icon: 'none',
                            duration: 2000
                        });
                        this.videoAd.show().catch(() => {
                            // 失败重试
                            this.videoAd.load()
                                .then(() => this.videoAd.show())
                                .catch(err => {
                                    console.error('激励视频广告显示失败', err);
                                });
                        });
                    }
                    break;
                default:
                    break;
            }
        },

        fabClick() {
           // 处理悬浮按钮的点击事件（可选）
          // 这里可以添加悬浮按钮本身的点击逻辑
        }
        // 以上是处理悬浮按钮的点击方法

    }
}
</script>

<style>
    .wrap {
      /* 设置背景图片 */
      background-image: url(/static/biao.png);
      background-size: cover;

      /* 设置容器大小和对齐方式 */
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100rpx;    /* 30vh */
    }

    .wrap2 {
      /* 设置背景图片 */
      background-image: url(/static/biao.png);
      background-size: cover;

      /* 设置容器大小和对齐方式 */
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100rpx;
      margin-top: -80rpx;
    }

    .nav_title {
      /* 设置文字颜色为透明，以便显示背景的渐变 */
      color: transparent;

      /* 应用线性渐变作为背景 */
      background: linear-gradient(to bottom, red, #f6c41a);

      /* 裁剪背景到文字 */
      -webkit-background-clip: text;

      /* 其他样式 */
      font-size: 46rpx;
      font-weight: bold;
    }
    .lnav{
        width: 320rpx;
        height: 160rpx;
        margin: 5rpx 15rpx 20rpx 33rpx;
        border-radius: 50rpx;
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
    }

    .page {
        height: 650rpx;
    }
    .page2 {
        height: 660rpx;
    }
    .nav-list {
        display: flex;
        flex-wrap: wrap;
        padding: 0px 40rpx 0px;
        justify-content: space-between;
    }

    .nav-li {
        padding: 30rpx;
        border-radius: 12rpx;
        width: 45%;
        margin: 0 2.5% 40rpx;
        /*   background-image: url(http://huanvip.cn/pic/975.png);   */
        background-size: cover;
        background-position: center;
        position: relative;
        z-index: 1;
    }

    .nav-li2 {
        padding: 30rpx;
        border-radius: 12rpx;
        width: 45%;
        margin: 0 2.5% 40rpx;
        /*   background-image: url(http://huanvip.cn/pic/975.png);   */
        background-size: cover;
        background-position: center;
        position: relative;
        z-index: 1;
        height: 110rpx;
    }

    .nav-li::after {
        content: "";
        position: absolute;
        z-index: -1;
        background-color: inherit;
        width: 100%;
        height: 100%;
        left: 0;
        bottom: -10%;
        border-radius: 10rpx;
        opacity: 0.2;
        transform: scale(0.9, 0.9);
    }

    .nav-li.cur {
        color: #fff;
        background: rgb(94, 185, 94);
        box-shadow: 4rpx 4rpx 6rpx rgba(94, 185, 94, 0.4);
    }

    .nav-title {
        font-size: 30rpx;
        font-weight: 300;
        font-weight: bold;
    }
    /*
    .nav-title::first-letter {
        font-size: 40rpx;
        margin-right: 4rpx;
    }
    */
    .nav-name {
        font-size: 28rpx;
        text-transform: Capitalize;
        margin-top: 20rpx;
        position: relative;
    }

    .nav-name::before {
        content: "";
        position: absolute;
        display: block;
        width: 40rpx;
        height: 6rpx;
        background: #fff;
        bottom: 0;
        right: 0;
        opacity: 0.5;
    }

    .nav-name::after {
        content: "";
        position: absolute;
        display: block;
        width: 100rpx;
        height: 1px;
        background: #fff;
        bottom: 0;
        right: 40rpx;
        opacity: 0.3;
    }

    .nav-name::first-letter {
        font-weight: bold;
        font-size: 36rpx;
        margin-right: 1px;
    }

    .nav-li text {
        position: absolute;
        right: 30rpx;
        top: 30rpx;
        font-size: 52rpx;
        width: 60rpx;
        height: 60rpx;
        text-align: center;
        line-height: 6rpx;
    }

    .text-light {
        font-weight: 300;
    }

    @keyframes show {
        0% {
            transform: translateY(-50px);
        }

        60% {
            transform: translateY(40rpx);
        }

        100% {
            transform: translateY(0px);
        }
    }

    @-webkit-keyframes show {
        0% {
            transform: translateY(-50px);
        }

        60% {
            transform: translateY(40rpx);
        }

        100% {
            transform: translateY(0px);
        }
    }
</style>    