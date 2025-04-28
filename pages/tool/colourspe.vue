<template>
  <view>
    <view class="biaoti">
      <uv-text text="变压器油样色谱分析三比值法计算" bold size="36rpx" align="center"></uv-text>
    </view>
    <view class="con">
      <view class="con1">
        <!-- 输入氢气含量 -->
        <view class="info">
          <text class="txt txtbiaoti" >氢气含量(H₂) </text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入氢气含量"
              v-model="H2"
              style="height: 65rpx;"
            />
          </view>
        </view>
        <!-- 输入甲烷含量 -->
        <view class="info">
          <text class="txt txtbiaoti" >甲烷含量(CH₄) </text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入甲烷含量"
              v-model="CH4"
              style="height: 65rpx;"
            />
          </view>
        </view>
        <!-- 输入乙烷含量 -->
        <view class="info">
          <text class="txt txtbiaoti" >乙烷含量(C₂H₆)</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入乙烷含量"
              v-model="C2H6"
              style="height: 65rpx;"
            />
          </view>
        </view>
        <!-- 输入乙烯含量 -->
        <view class="info">
          <text class="txt txtbiaoti" >乙烯含量(C₂H₄) </text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入乙烯含量"
              v-model="C2H4"
              style="height: 65rpx;"
            />
          </view>
        </view>
        <!-- 输入乙炔含量 -->
        <view class="info">
          <text class="txt txtbiaoti" >乙炔含量(C₂H₂) </text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入乙炔含量"
              v-model="C2H2"
              style="height: 65rpx;"
            />
          </view>
        </view>

        <!-- 显示三比值计算结果 -->
        <view class="info" style="border-color: red;">
          <text class="txt txtbiaoti" style="color: red;">三比值编码</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="text"
              placeholder="计算结果"
              v-model="ratioResult"
              disabled
              style="height: 65rpx;"
            />
          </view>
        </view>

        <!-- 显示分析结论 -->
        <view class="info" style="border-color: red;">
          <text class="txt txtbiaoti" style="color: red;">参考结论</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="text"
              placeholder="分析结果"
              v-model="analysisConclusion"
			  disabled
              style="height: 65rpx;"
            />
          </view>
        </view>

        <view class="info">
          <text class="txt txtgongshi">公式: C₂H₂/C₂H₄，CH₄/H₂，C₂H₄/C₂H₆</text>
        </view>
        <view class="info">
          <text class="txt txtgongshi" >注：单位均为μL/L</text>
        </view>
        <view style="display: flex; align-items: center; justify-content: center;">
          <button class="but1" @click="calculate">立即计算</button>
          <button class="but2" @click="clearAll">全部清空</button>
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
      shareTitle: '电气设备分析-变压器色谱分析三比值法计算', // 设置自定义的分享标题
      H2: null, // 氢气含量
      CH4: null, // 甲烷含量
      C2H6: null, // 乙烷含量
      C2H4: null, // 乙烯含量
      C2H2: null, // 乙炔含量

      ratioResult: null, // 三比值结果
      analysisConclusion: null, // 分析结论

      popupMessage: '', // 用于存储弹窗提示信息
    };
  },

  methods: {
    // 计算三比值法的方法
    calculate() {
      // 收集输入值
      const inputs = {
        H2: parseFloat(this.H2),
        CH4: parseFloat(this.CH4),
        C2H6: parseFloat(this.C2H6),
        C2H4: parseFloat(this.C2H4),
        C2H2: parseFloat(this.C2H2)
      };

      // 统计已输入值的数量
      const filledInputs = Object.values(inputs).filter(value => !isNaN(value)).length;

      if (filledInputs === 5) {
        // 调用计算函数
        const { ratioResult, conclusion } = calculateThreeRatios(inputs);
        this.ratioResult = ratioResult;
        this.analysisConclusion = conclusion;

      } else {
        this.popupMessage = '请输入所有气体含量值！'; // 设置提示信息
        this.$refs.popup.open(); // 打开弹窗
      }
    },

    // 清空方法
    clearAll() {
      this.H2 = null;
      this.CH4 = null;
      this.C2H6 = null;
      this.C2H4 = null;
      this.C2H2 = null;

      this.ratioResult = null;
      this.analysisConclusion = null;

      this.popupMessage = ''; // 清空提示信息
    }
  }
};

// 计算三比值和得出分析结论的函数
function calculateThreeRatios(inputs) {
  // 计算三个比值
  let ratio1 = inputs.C2H2 / inputs.C2H4;
  let ratio2 = inputs.CH4 / inputs.H2;
  let ratio3 = inputs.C2H4 / inputs.C2H6;

  // 根据比值结果计算结论
  if (ratio1 < 0.1) {
    ratio1 = 0;
  } else if (ratio1 >= 0.1 && ratio1 < 3) {
    ratio1 = 1;
  } else {
    ratio1 = 2;
  }

  if (ratio2 < 0.1) {
    ratio2 = 1;
  } else if (ratio2 >= 0.1 && ratio2 < 1) {
    ratio2 = 0;
  } else {
    ratio2 = 2;
  }

  if (ratio3 < 1) {
    ratio3 = 0;
  } else if (ratio3 >= 1 && ratio3 < 3) {
    ratio3 = 1;
  } else {
    ratio3 = 2;
  }

  // 根据比值结果设置分析结论
  let conclusion = '';
  if (ratio1 === 0 && ratio2 === 0 && ratio3 === 0) {
    conclusion = '低温过热(低于150℃)';
  } else if (ratio1 === 0 && ratio2 === 2 && ratio3 === 0) {
    conclusion = '低温过热(150-300℃)';
  } else if (ratio1 === 0 && ratio2 === 2 && ratio3 === 1) {
    conclusion = '中温过热(300-700℃)';
  } else if (ratio1 === 0 && (ratio2 === 2 || ratio2 === 1 || ratio2 === 0 ) && ratio3 === 2) {
    conclusion = '高温过热(高于700℃)';
  } else if (ratio1 === 0 && ratio2 === 1 && ratio3 === 0) {
    conclusion = '局部放电';
  } else if (ratio1 === 2 && (ratio2 === 1 || ratio2 === 0 ) && (ratio3 === 2 || ratio3 === 1 || ratio3 === 0 )) {
    conclusion = '低能放电';
  } else if (ratio1 === 2 && ratio2 === 2 && (ratio3 === 2 || ratio3 === 1 || ratio3 === 0 )) {
    conclusion = '低能放电兼过热';
  } else if (ratio1 === 1 && (ratio2 === 1 || ratio2 === 0 ) && (ratio3 === 2 || ratio3 === 1 || ratio3 === 0 )) {
    conclusion = '电弧放电';
  } else if (ratio1 === 1 && ratio2 === 2 && (ratio3 === 2 || ratio3 === 1 || ratio3 === 0 )) {
    conclusion = '电弧放电兼过热';
  } else {
    conclusion = '无法确定变压器状态';
  }

  // 返回比值结果和分析结论
  return {
    ratioResult: `${ratio1},${ratio2},${ratio3}`,
    conclusion
  };
}
</script>

<style>
/* 标题区域样式 */
.biaoti {
  width: 730rpx;
  display: flex;
  justify-content: space-between;
  background-color: #3c9cff; /* 蓝色背景 */
  margin: 5rpx 10rpx 0 10rpx; /* 外边距 */
  padding: 20rpx; /* 内边距 */
  border-radius: 30rpx 30rpx 0 0; /* 圆角，只设置顶部圆角 */
}

/* 主内容区域样式 */
.con {
  width: 730rpx;
  height: 100%;
  border: 2rpx solid #3c9cff; /* 蓝色边框 */
  margin: 0rpx 7rpx 0rpx 10rpx; /* 外边距 */
  padding: 0rpx; /* 内边距 */
  background-color: #9acafc;
  border-radius: 0 0 30rpx 30rpx; /* 圆角，只设置底部圆角 */
  font-size: 30rpx; /* 字体大小 */
  display: flex;
  flex-direction: column; /* 垂直排列子元素 */
}

/* 信息输入区域样式 */
.info {
  display: flex;
  height: auto;
  font-size: 36rpx; /* 字体大小 */
  justify-content: space-between; /* 子元素两端对齐 */
  padding: 0; /* 内边距 */
  margin: 20rpx 10rpx 20rpx 10rpx; /* 外边距 */
  border: 2rpx solid #808080; /* 灰色边框 */
  border-radius: 30rpx; /* 圆角 */
}

/* 输入框样式 */
.inp {
  width: 390rpx; /* 宽度 */
  height: 20rpx; /* 高度 */
  text-align: right; /* 文字右对齐 */
  margin-right: 10rpx; /* 右外边距 */
  border: none; /* 无边框 */
}

/* 标题文本样式 */
.txt {
  display: flex;
  align-items: center; /* 垂直居中 */
  justify-content: center; /* 水平居中 */
  height: 65rpx; /* 高度 */
  padding: 1rpx 10rpx 1rpx 10rpx; /* 内边距 */
}

/* 标题文本（标题）样式 */
.txtbiaoti {
  font-size: 34rpx; /* 字体大小 */
  background-color: #ecf5ff; /* 浅蓝色背景 */
  border-radius: 30rpx 0 0 30rpx; /* 圆角，左侧圆角 */
  width: 270rpx; /* 宽度 */
}

/* 公式文本样式 */
.txtgongshi {
  font-size: 34rpx; /* 字体大小 */
  width: auto; /* 自动宽度 */
  margin-left: 10rpx; /* 左外边距 */
}

/* 单位文本样式 */
.txtdanwei {
  font-weight: bold; /* 加粗 */
  font-size: 32rpx; /* 字体大小 */
}

/* 按钮样式 */
.but1, .but2 {
  margin-bottom: 20rpx; /* 下外边距 */
  height: 90rpx; /* 高度 */
  width: 240rpx; /* 宽度 */
  font-size: 36rpx; /* 字体大小 */
}

.but1 {
  background-color: rgb(58, 185, 158); /* 绿色背景 */
}
.but1:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
.but2 {
  background-color: #e45656; /* 红色背景 */
}
.but1:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
/* 弹窗样式 */
.uv-popup {
  background-color: #fff; /* 白色背景 */
  padding: 20rpx; /* 内边距 */
  border-radius: 10rpx; /* 圆角 */
  box-shadow: 0 0 10rpx rgba(0, 0, 0, 0.1); /* 阴影效果 */
}

/* 弹窗文本样式 */
.uv-popup text {
  font-size: 36rpx; /* 字体大小 */
  color: #333; /* 文字颜色 */
}
</style>