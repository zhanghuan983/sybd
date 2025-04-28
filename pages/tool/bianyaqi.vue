<template>
  <view>
    <!-- 直阻计算 -->
    <view class="biaoti">
      <uv-text text="变压器绕组直阻不平衡率计算：" bold size="34rpx"></uv-text>
      <navigator @click.stop.prevent="showOverlay" style="font-size: 30rpx;color: blue;">试验标准</navigator>
      <uv-icon name="question-circle"></uv-icon>
    </view>

    <!-- 直阻遮罩层 -->
    <view v-if="isOverlayVisible" class="overlay">
      <view class="overlay-content">
        <text class="overlay-text">
          <text style="font-weight: bold;">油浸式变压器、干式变压器及干式接地变直阻试验标准相同，</text>如下：\n
          ① <text style="text-decoration: underline;">1600kVA以上变压器</text>，各相绕组电阻相互间的差别不应大于三相平均值的2%，无中性点引出的绕组，线间差别不应大于三相平均值的1%；\n
          ② <text style="text-decoration: underline;">1600kVA及以下的变压器</text>，相间差别一般不大于三相平均值的4%，无中性点引出的绕组，线间差别一般不大于三相平均值的2%\n
          ③ 与以前相同部位测得值比较,其变化不应大于2%\n<text style="font-weight: bold;text-decoration: underline;">计算公式：不平衡率=(最大值-最小值)/平均值*100%</text>
        </text>
        <!-- 关闭按钮 -->
        <view class="close-button" @click="hideOverlay">
          <image src="../../static/tuichu.png" alt="关闭"></image>
        </view>
      </view>
    </view>

    <!-- 绝缘遮罩层 -->
    <view v-if="isOverJUEYUAN" class="overlay">
      <view class="overlay-content">
        <text class="overlay-text">
          <text style="font-weight: bold;">绕组绝缘电阻、吸收比试验标准：</text>\n
          <text style="font-weight: bold;"> 一、油浸式变压器要求：</text>\n
          ① <text style="font-weight: bold;">绝缘电阻换算至同一温度下，</text>与前一次测试结果相比应无显著变化，<text style="font-weight: bold;"> 不宜低于上次值的</text><text style="font-weight: bold;text-decoration: underline;">70%或不低于10000MΩ;</text>\n
          ② 电压等级为35kV及以上且容量在4000kVA及以上时，应测量吸收比。吸收比与产品出厂值比较无明显差别，在常温下不应小于1.3,当R60大于3000MΩ(20℃)时，吸收比可不作要求；\n
          ③ 电压等级为220kV及以上或容量为120MVA及以上时,宜用5000V兆欧表测量极化指数。测得值与产品出厂值比较无明显差别，在常温下不应小于1.5；当R60大于10000MΩ(20℃)时，极化指数可不作要求。\n
          <text style="font-weight: bold;">铁心、夹件绝缘电阻：</text>\n
          ① 220kV及以上:不宜低于500MΩ，110kV及以下:不宜低于100MΩ，66kV及以上:不宜低于100MΩ，35kV及以下:不宜低于10MΩ；\n
          ② 与以前测试结果相比无显著差别；\n
          ③ 运行中铁心接地电流不宜大于0.1A；\n
          ④ 运行中夹件接地电流不宜大于0.3A\n
          <text style="font-weight: bold;"> 二、干式变压器要求：\n绕组、铁心绝缘电阻换算至同一温度下，</text>与前一次测试结果相比应无显著变化，<text style="font-weight: bold;">  不宜低于上次值的70%。</text>
        </text>
        <!-- 关闭按钮 -->
        <view class="close-button" @click="hideOverlay1">
          <image src="../../static/tuichu.png" alt="关闭"></image>
        </view>
      </view>
    </view>

    <view class="con">
      <!-- 第一组单选框 -->
      <view class="radio-group-container">
        <text class="group-title">容量选择: </text>
        <uv-radio-group v-model="transformerCapacity" placement="row" style="display: flex; justify-content: flex-end;">
          <uv-radio name="smallCapacity" label="1.6MVA 及以下" :customStyle="{padding: '8rpx'}"></uv-radio>
          <uv-radio name="largeCapacity" label="1.6MVA 以上" :customStyle="{padding: '8rpx'}"></uv-radio>
        </uv-radio-group>
      </view>

      <!-- 第二组单选框 -->
      <view class="radio-group-container">
        <text class="group-title">请选择测量单位: </text>
        <uv-radio-group v-model="resistanceUnit" placement="row" style="display: flex; justify-content: flex-end;">
          <uv-radio name="milliOhm" label="mΩ" :customStyle="{padding: '8rpx'}"></uv-radio>
          <uv-radio name="microOhm" label="uΩ" :customStyle="{padding: '8rpx'}"></uv-radio>
          <uv-radio name="ohm" label="Ω" :customStyle="{padding: '8rpx'}"></uv-radio>
        </uv-radio-group>
      </view>

      <!-- 第三组单选框 -->
      <view class="radio-group-container">
        <text class="group-title">是否含有中性点: </text>
        <uv-radio-group v-model="hasNeutralPoint" placement="row" style="display: flex; justify-content: flex-end;">
          <uv-radio name="noNeutral" label="无" style="letter-spacing: 2rpx;" :customStyle="{padding: '8rpx'}"></uv-radio>
          <uv-radio name="hasNeutral" label="有" style="letter-spacing: 2rpx;" :customStyle="{padding: '8rpx'}"></uv-radio>
        </uv-radio-group>
      </view>
      <view class="input-group">
        <view class="input-item">
          <!-- 使用 v-if 指令根据 hasNeutralPoint 的值来动态显示不同的文本 -->
          <text v-if="hasNeutralPoint === 'noNeutral'" class="label">AB</text>
          <text v-if="hasNeutralPoint === 'hasNeutral'" class="label">AO</text>
          <text v-if="hasNeutralPoint === 'noNeutral'" class="label">BC</text>
          <text v-if="hasNeutralPoint === 'hasNeutral'" class="label">BO</text>
          <text v-if="hasNeutralPoint === 'noNeutral'" class="label">AC</text>
          <text v-if="hasNeutralPoint === 'hasNeutral'" class="label">CO</text>
          <input class="inp" v-model="input1" placeholder="请输入直阻" type="digit" clearable maxlength=8 />
          <input class="inp" v-model="input2" placeholder="请输入直阻" type="digit" clearable maxlength=8 />
          <input class="inp" v-model="input3" placeholder="请输入直阻" type="digit" clearable maxlength=8 />
        </view>
      </view>
      <view class="jieguo">
        <button @click="calculate" class="but1">立即计算</button>
        <text :class="resultClass" class="txt1">{{ result }}</text>
        <button @click="clearInputs" class="but2">清空</button>
      </view>
    </view>

    <!-- 吸收比计算 -->
    <view class="biaoti">
      <uv-text text="吸收比、极化指数计算：" bold size="34rpx"></uv-text>
      <navigator @click.stop.prevent="showOverlay1" style="font-size: 30rpx;color: blue;">试验标准</navigator>
      <uv-icon name="question-circle"></uv-icon>
    </view>
    <view class="con">
      <view class="input-group">
        <view class="input-item">
          <text class="label">15秒</text>
          <text class="label">60秒</text>
          <text class="label">600秒</text>
          <input class="inp" v-model="absorb15" placeholder="请输入" type="digit" clearable maxlength=8 />
          <input class="inp" v-model="absorb60" placeholder="请输入" type="digit" clearable maxlength=8 />
          <input class="inp" v-model="absorb600" placeholder="请输入" type="digit" clearable maxlength=8 />
        </view>
      </view>
      <view class="jieguo">
        <button @click="calculateAbsorbRatio" class="but1">立即计算</button>
        <text :class="absorbResultClass" class="txt1">{{ absorbResult }}</text>
        <button @click="clearAbsorbInputs" class="but2">清空</button>
      </view>
    </view>
  </view>
</template>

<script>
export default {
    data() {
        return {
            shareTitle: '变压器在线计算工具',
            hasNeutralPoint: 'noNeutral',
            resistanceUnit: 'milliOhm',
            transformerCapacity: 'smallCapacity',
            input1: '',
            input2: '',
            input3: '',
            result: '计算结果显示区域',
            resultClass: '',
            absorb15: '',
            absorb60: '',
            absorb600: '',
            absorbResult: '计算结果显示区域',
            absorbResultClass: '',
            isOverlayVisible: false, // 控制直阻遮罩层显示与隐藏
            isOverJUEYUAN: false, // 控制绝缘遮罩层显示与隐藏
        };
    },
    onLoad(options) {
        const paramMap = {};
        Object.keys(options).forEach(key => {
            paramMap[key] = decodeURIComponent(options[key] || '');
        });
    
        const {
            input1,
            input2,
            input3,
            result,
            hasNeutralPoint,
            resistanceUnit,
            transformerCapacity,
        } = paramMap;
    
        if (input1 && input2 && input3 && result && hasNeutralPoint && resistanceUnit && transformerCapacity) {
            this.input1 = input1;
            this.input2 = input2;
            this.input3 = input3;
            this.result = result;
            this.hasNeutralPoint = hasNeutralPoint;
            this.resistanceUnit = resistanceUnit;
            this.transformerCapacity = transformerCapacity;
        }
    },
    onShareAppMessage() {
        return {
            title: this.shareTitle,
            path: `/pages/tool/bianyaqi?input1=${encodeURIComponent(this.input1)}&input2=${encodeURIComponent(this.input2)}&input3=${encodeURIComponent(this.input3)}&result=${encodeURIComponent(this.result)}&hasNeutralPoint=${encodeURIComponent(this.hasNeutralPoint)}&resistanceUnit=${encodeURIComponent(this.resistanceUnit)}&transformerCapacity=${encodeURIComponent(this.transformerCapacity)}`
        };
    },
    onShareTimeline() {
        return {
            title: this.shareTitle,
            query: `input1=${encodeURIComponent(this.input1)}&input2=${encodeURIComponent(this.input2)}&input3=${encodeURIComponent(this.input3)}&result=${encodeURIComponent(this.result)}&hasNeutralPoint=${encodeURIComponent(this.hasNeutralPoint)}&resistanceUnit=${encodeURIComponent(this.resistanceUnit)}&transformerCapacity=${encodeURIComponent(this.transformerCapacity)}`
        };
    },
    methods: {
        calculate() {
            this.resultClass = '';

            const values = [parseFloat(this.input1), parseFloat(this.input2), parseFloat(this.input3)];
            if (values.some(isNaN)) {
                this.result = '请正确输入三相直阻！';
                this.resultClass = 'red-text red-border shake';
                return;
            }
            const max = Math.max(...values);
            const min = Math.min(...values);
            const avg = values.reduce((a, b) => a + b, 0) / values.length;
            const percentage = ((max - min) / avg) * 100;

            if (this.transformerCapacity === 'smallCapacity') {
                if (this.hasNeutralPoint === 'hasNeutral') {
                    if (percentage <= 4) {
                        this.result = `偏差：${percentage.toFixed(2)}%-合格`;
                        this.resultClass = 'green-text green-border shake';
                    } else {
                        this.result = `偏差：${percentage.toFixed(2)}%-不合格`;
                        this.resultClass = 'red-text red-border shake';
                    }
                } else {
                    if (percentage <= 2) {
                        this.result = `偏差：${percentage.toFixed(2)}%-合格`;
                        this.resultClass = 'green-text green-border shake';
                    } else {
                        this.result = `偏差：${percentage.toFixed(2)}%-不合格`;
                        this.resultClass = 'red-text red-border shake';
                    }
                }
            } else if (this.transformerCapacity === 'largeCapacity') {
                if (this.hasNeutralPoint === 'hasNeutral') {
                    if (percentage <= 2) {
                        this.result = `偏差：${percentage.toFixed(2)}%-合格`;
                        this.resultClass = 'green-text green-border shake';
                    } else {
                        this.result = `偏差：${percentage.toFixed(2)}%-不合格`;
                        this.resultClass = 'red-text red-border shake';
                    }
                } else {
                    if (percentage <= 1) {
                        this.result = `偏差：${percentage.toFixed(2)}%-合格`;
                        this.resultClass = 'green-text green-border shake';
                    } else {
                        this.result = `偏差：${percentage.toFixed(2)}%-不合格`;
                        this.resultClass = 'red-text red-border shake';
                    }
                }
            }
        },
        clearInputs() {
            this.input1 = '';
            this.input2 = '';
            this.input3 = '';
            this.result = '计算结果显示区域';
            this.resultClass = '';
        },
        calculateAbsorbRatio() {
            this.absorbResultClass = '';

            const values = [parseFloat(this.absorb15), parseFloat(this.absorb60), parseFloat(this.absorb600)];
            const absorbratio = values[1] / values[0];
            const abbratioppp = values[2] / values[1];
            this.absorbResult = `K:${absorbratio.toFixed(2)}—P:${abbratioppp.toFixed(2)}`;
            this.absorbResultClass = 'absorb-green-text green-border shake';
        },
        clearAbsorbInputs() {
            this.absorb15 = '';
            this.absorb60 = '';
            this.absorb600 = '';
            this.absorbResult = '计算结果显示区域';
            this.absorbResultClass = '';
        },
        showOverlay() {
            this.isOverlayVisible = true;
        },
        hideOverlay() {
            this.isOverlayVisible = false;
        },
        showOverlay1() {
            this.isOverJUEYUAN = true;
        },
        hideOverlay1() {
            this.isOverJUEYUAN = false;
        },
        // onShareAppMessage() {
        //     const encodedInput1 = encodeURIComponent(this.input1);
        //     const encodedInput2 = encodeURIComponent(this.input2);
        //     const encodedInput3 = encodeURIComponent(this.input3);
        //     const encodedResult = encodeURIComponent(this.result);
        //     const encodedHasNeutralPoint = encodeURIComponent(this.hasNeutralPoint);
        //     const encodedResistanceUnit = encodeURIComponent(this.resistanceUnit);
        //     const encodedTransformerCapacity = encodeURIComponent(this.transformerCapacity);

        //     return {
        //         title: this.shareTitle,
        //         path: `/pages/tool/bianyaqi?input1=${encodedInput1}&input2=${encodedInput2}&input3=${encodedInput3}&result=${encodedResult}&hasNeutralPoint=${encodedHasNeutralPoint}&resistanceUnit=${encodedResistanceUnit}&transformerCapacity=${encodedTransformerCapacity}`
        //     };
        // },
        // onShareTimeline() {
        //     const encodedInput1 = encodeURIComponent(this.input1);
        //     const encodedInput2 = encodeURIComponent(this.input2);
        //     const encodedInput3 = encodeURIComponent(this.input3);
        //     const encodedResult = encodeURIComponent(this.result);
        //     const encodedHasNeutralPoint = encodeURIComponent(this.hasNeutralPoint);
        //     const encodedResistanceUnit = encodeURIComponent(this.resistanceUnit);
        //     const encodedTransformerCapacity = encodeURIComponent(this.transformerCapacity);

        //     return {
        //         title: this.shareTitle,
        //         query: `input1=${encodedInput1}&input2=${encodedInput2}&input3=${encodedInput3}&result=${encodedResult}&hasNeutralPoint=${encodedHasNeutralPoint}&resistanceUnit=${encodedResistanceUnit}&transformerCapacity=${encodedTransformerCapacity}`
        //     };
        // }
    }
};
</script>

<style>
.biaoti {
  width: 730rpx;
  display: flex;
  justify-content: space-between;
  background-color: rgb(21, 191, 243);
  margin: 5rpx 10rpx 0 10rpx;
  padding: 20rpx 10rpx 20rpx 10rpx;
  border-radius: 30rpx 30rpx 0 0;
}

.con {
  width: 730rpx;
  background-color: rgb(222, 240, 254);
  border: 2rpx solid rgb(21, 191, 243);
  margin: 0rpx 7rpx 20rpx 10rpx;
  padding: 20rpx;
  border-radius: 0 0 30rpx 30rpx;
  font-size: 36rpx;
  display: flex;
  flex-direction: column;
}

.radio-group-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16rpx;
}

.group-title {
  display: inline-block;
  margin-right: 10rpx;
  padding: 6rpx;
  height: 35rpx;
  font-size: 32rpx;
}

.input-group {
  margin-bottom: 5px;
}

.input-item {
  display: flex;
  flex-wrap: wrap;
  width: 700rpx;
}

.label {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 220rpx;
  height: 90rpx;
  background-color: rgb(5, 205, 133);
  margin: 5rpx 5rpx 0 5rpx;
  border-radius: 25rpx 25rpx 0 0;
  font-size: 40rpx;
}

.inp {
  height: 90rpx;
  width: 220rpx;
  margin: 0 5rpx 0rpx 5rpx;
  border: 3rpx solid black;
  border-radius: 0 0 25rpx 25rpx;
  text-align: center;
}

.but1 {
  width: 180rpx;
  height: 90rpx;
  background-color: rgb(58, 185, 158);
  border-radius: 5rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30rpx;
  font-weight: bold;
  margin: 15rpx 5rpx 15rpx 10rpx;
}
.but1:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
.but2 {
  width: 120rpx;
  height: 90rpx;
  background-color: #e45656;
  border-radius: 30rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30rpx;
  margin: 15rpx 5rpx 15rpx 5rpx;
}

.txt1 {
  width: 350rpx;
  height: 88rpx;
  border: 2rpx solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30rpx;
  border-radius: 25rpx 25rpx 25rpx 25rpx;
  margin: 15rpx 5rpx 15rpx 5rpx;
}

.green-text {
  color: green;
}

.red-text {
  color: red;
}

.jieguo {
  display: flex;
}

/* 以下是结果显示区域的动态 css */
@keyframes shake {
  0% {
    transform: translate(1px, 1px) rotate(0deg);
  }
  10% {
    transform: translate(-1px, -2px) rotate(-1deg);
  }
  20% {
    transform: translate(-3px, 0px) rotate(1deg);
  }
  30% {
    transform: translate(3px, 2px) rotate(0deg);
  }
  40% {
    transform: translate(1px, -1px) rotate(1deg);
  }
  50% {
    transform: translate(-1px, 2px) rotate(-1deg);
  }
  60% {
    transform: translate(-3px, 1px) rotate(0deg);
  }
  70% {
    transform: translate(3px, 1px) rotate(-1deg);
  }
  80% {
    transform: translate(-1px, -1px) rotate(1deg);
  }
  90% {
    transform: translate(1px, 2px) rotate(0deg);
  }
  100% {
    transform: translate(1px, -2px) rotate(-1deg);
  }
}

.shake {
  animation: shake 0.5s;
  animation-iteration-count: 1.5; /* 晃动 2 次 */
}

/* 以上是结果显示区域的动态 css */
/* 以下是结果显示区域的边框样式 */
.green-border { 
  border: 2rpx solid green;
}

.red-border {
  border: 2rpx solid red;
}

/* 吸收比计算结果样式 */
.absorb-green-text {
  color: green;
}

.absorb-red-text {
  color: red;
}

.absorb-jieguo {
  display: flex;
}

/* 遮罩层样式 */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* 半透明黑色背景 */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000; /* 确保遮罩层在最上层 */
}

/* 遮罩层内容样式 */
.overlay-content {
  background-color: white;
  padding: 20rpx;
  border-radius: 10rpx;
  text-align: left;
  position: relative; /* 相对定位 */
  max-width: 80%; /* 限制内容最大宽度 */
  box-sizing: border-box; /* 包括内边距和边框在内的宽度计算 */
  overflow: auto; /* 添加滚动条 */
  max-height: 80vh; /* 设置最大高度为视口高度的80% */
}

/* 遮罩层内文字样式 */
.overlay-text {
  font-size: 32rpx; /* 增大文字大小 */
  margin-bottom: 10rpx;
}

/* 关闭按钮样式 */
.close-button {
  position: absolute;
  top: 0rpx; /* 调整top值以适应图片大小 */
  right: 0rpx; /* 调整right值以适应图片大小 */
  width: 45rpx; /* 根据图片大小调整 */
  height: 45rpx; /* 根据图片大小调整 */
  cursor: pointer;
}

/* 关闭按钮的图片样式 */
.close-button image {
  width: 100%;
  height: 100%;
}
</style>
