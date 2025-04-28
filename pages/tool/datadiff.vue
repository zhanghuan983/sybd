<template>
  <view>
    <view class="biaoti">
      <uv-text text="试验数据初值差计算" bold size="36rpx" align="center"></uv-text>
    </view>
    <view class="con"> 
      <view  class="con1">
        <view class="info">
          <text class="txt txtbiaoti" :style="{ color: t1Color }">上次试验数值</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入上次数据"
              v-model="chu"
              style="height: 65rpx;"
            />  
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti" :style="{ color: t2Color }">本次试验数值</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入本次数据"
              v-model="ben"
              style="height: 65rpx;"
            />
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti" :style="{ color: R1Color }">初值差</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="计算结果"
              v-model="cha"
			  disabled
              style="height: 65rpx;"
            />
            <text class="txt txtdanwei">%</text>
          </view>
        </view>
        
        <view class="info">
          <text class="txt txtgongshi">公式:初值差=(本次值-初值)/初值*100%</text>
        </view>
        <view class="info">
          <text class="txt txtgongshi" >注：请至少输入任意三个值再计算!</text>
        </view>
        <view style="display: flex; align-items: center; justify-content: center;">
          <button class="but1" @click="calcu">立即计算</button>
          <button class="but2" @click="clear">全部清空</button>
        </view>
      </view>
	  
	  <!-- 添加uv-popup组件用于提示 -->
	  <uv-popup ref="popup" mode="center" round="10" closeable="true">
	    <view style="height: 100rpx; display: flex; align-items: center; justify-content: center;">
	      <text style="width: auto; height: auto; font-size: 36rpx; margin: 80rpx;">{{ popupMessage }}</text>
	    </view>
	  </uv-popup>
    </view>
  </view>
</template>

<script>
import { shareMixin } from '/shareMixin.js';

export default {
  mixins: [shareMixin],
  data() {
    return {
		shareTitle: '电气试验宝典-试验数据初值差计算', // 设置自定义的分享标题
        chu: null, // 初值
        ben: null, // 本次
        cha: null, // 初值差
        popupMessage : '请输入初值和本次值！',
		// 状态控制，用于改变标题文字颜色
		t1Color: 'black', // 标题颜色
		t2Color: 'black', // 标题颜色
		R1Color: 'black', //  标题颜色
		
      };
  },
  
  methods: {
    // 计算初值差的方法
        calcu() {
            // 收集输入值
            const inputs = {
                chu: parseFloat(this.chu),
                ben: parseFloat(this.ben),
            };
    
            // 统计已输入值的数量
            const filledInputs = Object.values(inputs).filter(value => !isNaN(value)).length;
    
            if (filledInputs === 2) {
                if (inputs.chu === 0) {
                    this.popupMessage = '初值不能为零！';
                    this.$refs.popup.open();
                    return;
                }
    
                // 计算初值差
                const cha = ((inputs.ben - inputs.chu) / inputs.chu) * 100;
                this.cha = cha.toFixed(4); // 保留四位小数
    
                // 设置标题文字颜色为红色
                this.R1Color = 'red';
            } else {
                this.popupMessage = '请输入初值和本次值！';
                this.$refs.popup.open();
            }
        },
		// 清空方法
		clear() {
		  this.ben = null;
		  this.chu = null;
		  this.cha = null;
		  
		// 重置标题文字颜色
		  this.t1Color = 'black';
		  this.t2Color = 'black';
		  this.R1Color = 'black';
		  
		},
	}
};
</script>

<style>
.biaoti {
  width: 730rpx;
  display: flex;
  justify-content: space-between;
  background-color: #3c9cff;
  margin: 5rpx 10rpx 0 10rpx;
  padding: 20rpx;
  border-radius: 30rpx 30rpx 0 0;
}

.con {
  width: 730rpx;
  height: 100%;
  border: 2rpx solid #3c9cff;
  margin: 0rpx 7rpx 0rpx 10rpx;
  padding: 0rpx;
  border-radius: 0 0 30rpx 30rpx;
  font-size: 30rpx;
  display: flex;
  flex-direction: column;
}

.tab-bar {
  width: 722rpx;
  display: flex;
  justify-content: space-around;
  background-color: white;
  margin: 0rpx;
}

.tab-item {
  cursor: pointer;
  border: 1rpx solid black;
  border-radius: 50rpx;
  padding: 16rpx;
  margin: 6rpx 6rpx 8rpx 6rpx;
  background-color: #9acafc;
}

.active {
  font-weight: bold;
  border: 0;
  border-radius: 30rpx 30rpx 0 0;
  background-color: #9acafc;
  margin: 5rpx 5rpx 0 5rpx;
  font-size: 34rpx;
  border-top: 2rpx solid #3c9cff;
  border-left: 2rpx solid #3c9cff;
  border-right: 2rpx solid #3c9cff;
  z-index: 10;
}

.con1 {
  height: 100%;
  padding: 0 5rpx 5rpx 5rpx;
  margin: -2rpx 0;
  background-color: #9acafc;
  border-radius: 0rpx 0rpx 30rpx 30rpx;
  border: 2rpx solid #3c9cff;
}

.info {
  display: flex;
  height: auto;
  font-size: 36rpx;
  justify-content: space-between;
  padding: 0; /* 10rpx 20rpx 10rpx 20rpx */
  margin: 20rpx 10rpx 20rpx 10rpx;
  border: 2rpx solid #808080;
  border-radius: 30rpx;
}

.inp {
  width: 300rpx;
  height: 20rpx;
  text-align: right;
  margin-right: 10rpx;
  border: none;
  
}

.txt {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 65rpx;
  padding: 1rpx 10rpx 1rpx 10rpx;
}

.txtbiaoti {
  font-size: 34rpx;
  background-color: #ecf5ff;
  border-radius: 30rpx 0 0 30rpx;
  width: 270rpx;
}

.txtgongshi {
  font-size: 34rpx;
  width: auto;
  margin-left: 10rpx;
}

.txtdanwei {
  font-weight: bold;
  font-size: 32rpx;
}

.but1 {
  margin-bottom: 20rpx;
  background-color: rgb(58, 185, 158);
  height: 90rpx;
  width: 240rpx;
  font-size: 36rpx;
}

.but2 {
  margin-bottom: 20rpx;
  background-color: #e45656;
  height: 90rpx;
  width: 240rpx;
  font-size: 36rpx;
}
.but1:active:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
.but2:active:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
</style>
