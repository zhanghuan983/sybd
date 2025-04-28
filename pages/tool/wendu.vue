<template>
  <view>
    <view class="biaoti">
      <uv-text text="温度换算工具" bold size="36rpx" align="center"></uv-text>
    </view>
    <view class="con">
      <view class="tab-bar">
        <view
          class="tab-item"
          :class="{ active: tab1 === 'R' }"
          @click="tab1 = 'R'"
        >
          直流电阻
        </view>
		<view
		  class="tab-item"
		  :class="{ active: tab1 === 'R2' }"
		  @click="tab1 = 'R2'"
		>
		  绝缘电阻
		</view>
		<view
		  class="tab-item"
		  :class="{ active: tab1 === 'R3' }"
		  @click="tab1 = 'R3'"
		>
		  介损因数
		</view>
      </view>
      <view v-if="tab1 === 'R'" class="con1">
        <!-- 以下是直流电阻温度换算相关内容 -->
        <view class="info">
          <text class="txt txtbiaoti">请选择材质</text>
          <view style="display: flex; justify-content: flex-end; padding-top: 8rpx; padding-right: 10rpx;">
            <radio-group @change="handleMaterialChange">
              <label>
                <radio value="copper" :checked="material === 'copper'"/>铜
              </label>
              <label>
                <radio value="aluminum" :checked="material === 'aluminum'"/>铝
              </label>
            </radio-group>
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti" :style="{ color: t1Color }">测量温度(t1)</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入现在温度"
              v-model="t1Input"
              style="height: 65rpx;"
            />
            <text class="txt txtdanwei">°C&nbsp;&nbsp;&nbsp;</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti" :style="{ color: t2Color }">换算温度(t2)</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入换算温度"
              v-model="t2Input"
              style="height: 65rpx;"
            />
            <text class="txt txtdanwei">°C&nbsp;&nbsp;&nbsp;</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti" :style="{ color: R1Color }">测量电阻(R1)</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入测量电阻"
              v-model="R1Input"
              style="height: 65rpx;"
            />
            <text class="txt txtdanwei">mΩ</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti" :style="{ color: R2Color }">换算电阻(R2)</text>
          <view style="display: flex; justify-content: flex-end;">
            <input
              class="inp"
              type="digit"
              maxlength="10"
              placeholder="请输入换算电阻"
              v-model="R2Input"
              style="height: 65rpx;"
            />
            <text class="txt txtdanwei">mΩ</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtgongshi">计算公式：R2 = R1 * (T + t2) / (T + t1)</text>
        </view>
        <view class="info">
          <text class="txt txtgongshi" >注：请至少输入任意三个值再计算!</text>
        </view>
        <view style="display: flex; align-items: center; justify-content: center;">
          <button class="but1" @click="calculateR2">立即计算</button>
          <button class="but2" @click="clearInputs2">全部清空</button>
        </view>
      </view>
	  
	  <view v-if="tab1 === 'R2'" class="con1">
	    <!-- 以下是绝缘电阻温度换算相关内容 -->
	    
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: R2t1Color }">测量温度(t1)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入现在温度"
	          v-model="R2t1Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">°C </text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: R2t2Color }">换算温度(t2)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入换算温度"
	          v-model="R2t2Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">°C </text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: R2R1Color }">测量电阻(R1)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入测量电阻"
	          v-model="R2R1Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">Ω</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: R2R2Color }">换算电阻(R2)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入换算电阻"
	          v-model="R2R2Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">Ω</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtgongshi">计算公式：R2 = R1*1.5^((t1-t2)/10)</text>
	    </view>
	    <view class="info">
	      <text class="txt txtgongshi" >注：请至少输入任意三个值再计算!</text>
	    </view>
	    <view style="display: flex; align-items: center; justify-content: center;">
	      <button class="but1" @click="calculateR2R2">立即计算</button>
	      <button class="but2" @click="clearInputsR2">全部清空</button>
	    </view>
	  </view>
	  
	  <view v-if="tab1 === 'R3'" class="con1">
	    <!-- 以下是介损因数计算相关内容 -->
	    
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: tant1Color }">测量温度(t1)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入现在温度"
	          v-model="Dt1Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">°C</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: tant2Color }">换算温度(t2)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入换算温度"
	          v-model="Dt2Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">°C</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: tan1Color }">测量介损(tanδ₁)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入测量介损"
	          v-model="Dtan1Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">%</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti" :style="{ color: tan2Color }">换算介损(tanδ₂)</text>
	      <view style="display: flex; justify-content: flex-end;">
	        <input
	          class="inp"
	          type="digit"
	          maxlength="10"
	          placeholder="请输入换算介损"
	          v-model="Dtan2Input"
	          style="height: 65rpx;"
	        />
	        <text class="txt txtdanwei">%</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtgongshi">计算公式：tanδ₂=tanδ₁*1.3^((t2-t1)/10)</text>
	    </view>
	    <view class="info">
	      <text class="txt txtgongshi" >注：请至少输入任意三个值再计算!</text>
	    </view>
	    <view style="display: flex; align-items: center; justify-content: center;">
	      <button class="but1" @click="calculateDtan2">立即计算</button>
	      <button class="but2" @click="clearInputs3">全部清空</button>
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
		shareTitle: '电气试验宝典-温度换算在线计算工具', // 设置自定义的分享标题
        tab1: 'R',
        t1Input: null, // 直阻测量温度 (t1)
        t2Input: null, // 直阻换算温度 (t2)
        R1Input: null, // 直阻测量电阻 (R1)
        R2Input: null, // 直阻换算电阻 (R2)
        material: 'copper', // 设置初始值为'copper'，即默认选中铜
        
        R2t1Input: null, // 绝缘测量温度 (t1)
        R2t2Input: null, // 绝缘换算温度 (t2)
        R2R1Input: null, // 绝缘测量电阻 (R1)
        R2R2Input: null, // 绝缘换算电阻 (R2)
		
		// 介损因数相关数据
		Dt1Input: null, // 介损测量温度 (t1)
		Dt2Input: null, // 介损换算温度 (t2)
		Dtan1Input: null, // 介损测量介损 (tanδ₁)
		Dtan2Input: null, // 介损换算介损 (tanδ₂)
		popupMessage: '',
		
		// 状态控制，用于改变标题文字颜色
		t1Color: 'black', // 直阻测量温度 (t1) 标题颜色
		t2Color: 'black', // 直阻换算温度 (t2) 标题颜色
		R1Color: 'black', // 直阻测量电阻 (R1) 标题颜色
		R2Color: 'black', // 直阻换算电阻 (R2) 标题颜色
		R2t1Color: 'black', // 绝缘测量温度 (t1) 标题颜色
		R2t2Color: 'black', // 绝缘换算温度 (t2) 标题颜色
		R2R1Color: 'black', // 绝缘测量电阻 (R1) 标题颜色
		R2R2Color: 'black', // 绝缘换算电阻 (R2) 标题颜色
		tant1Color: 'black', // 介损测量温度 (t1) 标题颜色
		tant2Color: 'black', // 介损换算温度 (t2) 标题颜色
		tan1Color: 'black', // 介损因数(tan1) 标题颜色
		tan2Color: 'black', // 介损因数(tan2) 标题颜色
      };
  },
  
  methods: {
    // 处理材质选择变化的方法
    handleMaterialChange(e) {
      this.material = e.detail.value;
    },
  
    // 计算直流电阻换算电阻的方法
    calculateR2() {
      // 收集直流电阻输入值
      const inputs = {
        t1: parseFloat(this.t1Input),
        t2: parseFloat(this.t2Input),
        R1: parseFloat(this.R1Input),
        R2: parseFloat(this.R2Input),
      };
  
      // 根据材质设置 T 值
      let T;
      if (this.material === 'copper') {
        T = 235;
      } else if (this.material === 'aluminum') {
        T = 225;
      } else {
        this.popupMessage = '请选择有效的材质！';
        this.$refs.popup.open();
        return;
      }
  
      // 计算缺失的直流电阻值
      let calculatedValue = null;
      let calculatedField = null;
  
      // 统计已输入值的数量
      const filledInputs = Object.values(inputs).filter(value => !isNaN(value)).length;
  
      if (filledInputs === 4) {
        // 如果四个输入框都有值，计算 R2
        calculatedValue = inputs.R1 * (T + inputs.t2) / (T + inputs.t1);
        calculatedField = 'R2';
      } else if (filledInputs === 3) {
        if (isNaN(inputs.R2)) {
          // 计算 R2
          calculatedValue = inputs.R1 * (T + inputs.t2) / (T + inputs.t1);
          calculatedField = 'R2';
        } else if (isNaN(inputs.R1)) {
          // 计算 R1
          calculatedValue = inputs.R2 * (T + inputs.t1) / (T + inputs.t2);
          calculatedField = 'R1';
        } else if (isNaN(inputs.t2)) {
          // 计算 t2
          calculatedValue = (inputs.R2 * (T + inputs.t1)) / inputs.R1 - T;
          calculatedField = 't2';
        } else if (isNaN(inputs.t1)) {
          // 计算 t1
          calculatedValue = (inputs.R1 * (T + inputs.t2)) / inputs.R2 - T;
          calculatedField = 't1';
        }
      } else {
        this.popupMessage = '请输入至少三个值！';
        this.$refs.popup.open();
        return;
      }
  
      if (calculatedValue !== null && calculatedField !== null) {
        // 设置直流电阻计算结果
        this[calculatedField + 'Input'] = calculatedValue.toFixed(4);
        // 设置标题文字颜色为红色
        if (calculatedField === 't1') {
          this.t1Color = 'red';
        } else if (calculatedField === 't2') {
          this.t2Color = 'red';
        } else if (calculatedField === 'R1') {
          this.R1Color = 'red';
        } else if (calculatedField === 'R2') {
          this.R2Color = 'red';
        }
      } else {
        this.popupMessage = '无法计算，请检查输入值！';
        this.$refs.popup.open();
      }
    },
  
    // 计算绝缘电阻换算电阻的方法
    calculateR2R2() {
      // 收集绝缘电阻输入值
      const inputs = {
        t1: parseFloat(this.R2t1Input),
        t2: parseFloat(this.R2t2Input),
        R1: parseFloat(this.R2R1Input),
        R2: parseFloat(this.R2R2Input),
      };
  
      // 计算缺失的绝缘电阻值
      let calculatedValue = null;
      let calculatedField = null;
  
      // 统计已输入值的数量
      const filledInputs = Object.values(inputs).filter(value => !isNaN(value)).length;
  
      if (filledInputs === 4) {
        // 如果四个输入框都有值，计算 R2
        calculatedValue = inputs.R1 * Math.pow(1.5, (inputs.t1 - inputs.t2) / 10);
        calculatedField = 'R2';
      } else if (filledInputs === 3) {
        if (isNaN(inputs.R2)) {
          // 计算 R2
          calculatedValue = inputs.R1 * Math.pow(1.5, (inputs.t1 - inputs.t2) / 10);
          calculatedField = 'R2';
        } else if (isNaN(inputs.R1)) {
          // 计算 R1
          calculatedValue = inputs.R2 / Math.pow(1.5, (inputs.t1 - inputs.t2) / 10);
          calculatedField = 'R1';
        } else if (isNaN(inputs.t2)) {
          // 计算 t2
          calculatedValue = inputs.t1 - 10 * Math.log(inputs.R2 / inputs.R1) / Math.log(1.5);
          calculatedField = 't2';
        } else if (isNaN(inputs.t1)) {
          // 计算 t1
          calculatedValue = inputs.t2 + 10 * Math.log(inputs.R2 / inputs.R1) / Math.log(1.5);
          calculatedField = 't1';
        }
      } else {
        this.popupMessage = '请输入至少三个值！';
        this.$refs.popup.open();
        return;
      }
  
      if (calculatedValue !== null && calculatedField !== null) {
        // 设置绝缘电阻计算结果
        this['R2' + calculatedField + 'Input'] = calculatedValue.toFixed(4);
        // 设置标题文字颜色为红色
        if (calculatedField === 't1') {
          this.R2t1Color = 'red';
        } else if (calculatedField === 't2') {
          this.R2t2Color = 'red';
        } else if (calculatedField === 'R1') {
          this.R2R1Color = 'red';
        } else if (calculatedField === 'R2') {
          this.R2R2Color = 'red';
        }
      } else {
        this.popupMessage = '无法计算，请检查输入值！';
        this.$refs.popup.open();
      }
    },
	
	// 计算介损因数换算介损的方法
	calculateDtan2() {
	  // 收集介损因数输入值
	  const inputs = {
	    t1: parseFloat(this.Dt1Input), // 测量温度 (t1)
	    t2: parseFloat(this.Dt2Input), // 换算温度 (t2)
	    tan1: parseFloat(this.Dtan1Input), // 测量介损 (tanδ₁)
	    tan2: parseFloat(this.Dtan2Input), // 换算介损 (tanδ₂)
	  };
	
	  // 计算缺失的介损因数值
	  let calculatedValue = null;
	  let calculatedField = null;
	
	  // 统计已输入值的数量
	  const filledInputs = Object.values(inputs).filter(value => !isNaN(value)).length;
	
	  if (filledInputs === 4) {
	    // 如果四个输入框都有值，计算 tanδ₂
	    calculatedValue = inputs.tan1 * Math.pow(1.3, (inputs.t2 - inputs.t1) / 10);
	    calculatedField = 'tan2';
	  } else if (filledInputs === 3) {
	    if (isNaN(inputs.tan2)) {
	      // 计算 tanδ₂
	      calculatedValue = inputs.tan1 * Math.pow(1.3, (inputs.t2 - inputs.t1) / 10);
	      calculatedField = 'tan2';
	    } else if (isNaN(inputs.tan1)) {
	      // 计算 tanδ₁
	      calculatedValue = inputs.tan2 / Math.pow(1.3, (inputs.t2 - inputs.t1) / 10);
	      calculatedField = 'tan1';
	    } else if (isNaN(inputs.t2)) {
	      // 计算 t2
	      calculatedValue = inputs.t1 + 10 * Math.log(inputs.tan2 / inputs.tan1) / Math.log(1.3);
	      calculatedField = 't2';
	    } else if (isNaN(inputs.t1)) {
	      // 计算 t1
	      calculatedValue = inputs.t2 - 10 * Math.log(inputs.tan2 / inputs.tan1) / Math.log(1.3);
	      calculatedField = 't1';
	    }
	  } else {
	    this.popupMessage = '请输入至少三个值！';
	    this.$refs.popup.open();
	    return;
	  }
	
	  if (calculatedValue !== null && calculatedField !== null) {
	    // 设置介损因数计算结果
	    this['D' + calculatedField + 'Input'] = calculatedValue.toFixed(4);
	    // 设置标题文字颜色为红色
	    if (calculatedField === 't1') {
	      this.tant1Color = 'red';
	    } else if (calculatedField === 't2') {
	      this.tant2Color = 'red';
	    } else if (calculatedField === 'tan1') {
	      this.tan1Color = 'red';
	    } else if (calculatedField === 'tan2') {
	      this.tan2Color = 'red';
	    }
	  } else {
	    this.popupMessage = '无法计算，请检查输入值！';
	    this.$refs.popup.open();
	  }
	},
	
	// 清空直流电阻输入的方法
	clearInputs2() {
	  this.t1Input = null;
	  this.t2Input = null;
	  this.R1Input = null;
	  this.R2Input = null;
	  this.material = 'copper'; // 重置材质为铜
	 // 重置标题文字颜色
	 this.t1Color = 'black';
	 this.t2Color = 'black';
	 this.R1Color = 'black';
	 this.R2Color = 'black';
	 this.materialColor = 'black';
	},
	  
	// 清空绝缘电阻输入的方法
	clearInputsR2() {
	  this.R2t1Input = null;
	  this.R2t2Input = null;
	  this.R2R1Input = null;
	  this.R2R2Input = null;
	// 重置标题文字颜色
	  this.R2t1Color = 'black';
	  this.R2t2Color = 'black';
	  this.R2R1Color = 'black';
	  this.R2R2Color = 'black';
	  this.materialColor = 'black';
	},
	
	// 清空介质因数输入的方法
	clearInputs3() {
	  this.Dt1Input = null;
	  this.Dt2Input = null;
	  this.Dtan1Input = null;
	  this.Dtan2Input = null;
	// 重置标题文字颜色
	  this.tant1Color = 'black';
	  this.tant2Color = 'black';
	  this.tan1Color = 'black';
	  this.tan2Color = 'black';
	},
	
	
  }, 
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
  border-radius: 20rpx 20rpx 30rpx 30rpx;
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
.but1:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
.but2 {
  margin-bottom: 20rpx;
  background-color: #e45656;
  height: 90rpx;
  width: 240rpx;
  font-size: 36rpx;
}
.but2:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
</style>
