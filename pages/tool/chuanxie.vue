<template>
  <view>
    <view class="biaoti">
      <uv-text text="变频串联谐振选型神器" bold size="36rpx" align="center"></uv-text>
    </view>
    <view class="con">
      <view class="tab-bar">
        <view
          class="tab-item"
          :class="{ active: tab1 === 'F' }"
          @click="tab1 = 'F'"
        >
          计算频率
        </view>
        <view
          class="tab-item"
          :class="{ active: tab1 === 'C' }"
          @click="tab1 = 'C'"
        >
          计算电容
        </view>
        <view
          class="tab-item"
          :class="{ active: tab1 === 'L' }"
          @click="tab1 = 'L'"
        >
          计算电感
        </view>
      </view>
	  
      <view v-if="tab1 === 'F'" class="con1">      <!-- 以下是计算电容 -->
        <view class="info">
          <text class="txt txtbiaoti">电感（L）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="请输入电感" v-model="LInput" style="height: 65rpx;"/>
            <text class="txt txtdanwei">H&nbsp;</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti">电容（C）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="请输入电容" v-model="CInput" style="height: 65rpx;"/>
            <text class="txt txtdanwei">μF</text>
          </view>
        </view>
        <view class="info" style="border: 2rpx solid red;">
          <text class="txt txtbiaoti " style="color:red">频率（F）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit"  maxlength=10 placeholder="点击计算查看结果" disabled placeholder-style="color:red;" style="color:red;height: 65rpx;" v-model="FInput" />
            <text class="txt txtdanwei" style="color: red;">Hz</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtgongshi">计算公式：F=1/(2π*(LC)^(1/2))</text>
        </view>
        <view class="info">
          <text class="txt txtgongshi" >注：请注意输入值的单位!</text>
        </view>
        <view style="display: flex;align-items: center;justify-content: center;">
          <button class="but1" @click="calculateF">立即计算</button>
          <button class="but2" @click="clearInputs2">全部清空</button>
        </view>
      </view>
      
      <view v-if="tab1 === 'C'" class="con1">      <!-- 以下是计算电容 -->
        <view class="info">
          <text class="txt txtbiaoti">电感（L）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="请输入电感" v-model="LInput" style="height: 65rpx;"/>
            <text class="txt txtdanwei">H&nbsp;</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti">频率（F）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="请输入频率" v-model="FInput" style="height: 65rpx;"/>
            <text class="txt txtdanwei">Hz</text>
          </view>
        </view>
        <view class="info" style="border: 2rpx solid red;">
          <text class="txt txtbiaoti" style="color: red;">电容（C）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="点击计算查看结果" disabled placeholder-style="color:red;" style="color:red;height: 65rpx;"  v-model="CInput" />
            <text class="txt txtdanwei" style="color: red;">μF</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtgongshi">计算公式：C=1/((2π*F)²*L)</text>
        </view>
        <view class="info">
          <text class="txt txtgongshi" >注：请注意输入值的单位!</text>
        </view>
        <view style="display: flex;align-items: center;justify-content: center;">
          <button class="but1" @click="calculateC">立即计算</button>
          <button class="but2" @click="clearInputs2">全部清空</button>
        </view>
      </view>
	  
      <view v-if="tab1 === 'L'" class="con1">      <!-- 以下是计算电感 -->
        <view class="info">
          <text class="txt txtbiaoti">频率（F）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="请输入频率" v-model="FInput" style="height: 65rpx;"/>
            <text class="txt txtdanwei">Hz</text>
          </view>
        </view>
        <view class="info">
          <text class="txt txtbiaoti">电容（C）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="请输入电容" v-model="CInput" style="height: 65rpx;"/>
            <text class="txt txtdanwei">μF</text>
          </view>
        </view>
        <view class="info" style="border: 2rpx solid red;">
          <text class="txt txtbiaoti" style="color: red;">电感（L）</text>
          <view style="display: flex;justify-content: flex-end;">
            <input class="inp" type="digit" maxlength=10 placeholder="点击计算查看结果" disabled placeholder-style="color:red;" style="color:red;height: 65rpx;"  v-model="LInput" />
            <text class="txt txtdanwei" style="color: red;">H&nbsp;</text>
          </view>
        </view>
        <view class="info">
			<text class="txt txtgongshi">计算公式：L=1/((2π*F)²*C)</text>
        </view>
        <view class="info">
          <text class="txt txtgongshi" >注：请注意输入值的单位!</text>
        </view>
        <view style="display: flex;align-items: center;justify-content: center;">
          <button class="but1" @click="calculateL">立即计算</button>
          <button class="but2" @click="clearInputs2">全部清空</button>
        </view>
      </view>
      <!-- 添加uv-popup组件用于提示 -->
      <uv-popup ref="popup" mode="center" round="10" closeable="true">
        <view style="height: 100rpx;display: flex;align-items: center;justify-content: center;">
          <text style="width: auto;height: auto;font-size: 36rpx;margin: 80rpx;">{{ popupMessage }}</text>
        </view>
      </uv-popup>
    </view>
	<view class="biaoti">
	  <uv-text text="变频串联谐振选型神器" bold size="36rpx" align="center"></uv-text>
	</view>
	<view class="con">
	  <view class="tab-bar">
	    
	    <view
	      class="tab-item"
	      :class="{ active: tab2 === 'dianliu' }"
	      @click="tab2 = 'dianliu'"
	    >
	      计算电流
	    </view>
	    
	    <view
	      class="tab-item"
	      :class="{ active: tab2 === 'qqq' }"
	      @click="tab2 = 'qqq'"
	    >
	      计算品质因数
	    </view>
	  </view>
	  
	  <view v-if="tab2 === 'dianliu'" class="con1">      <!-- 以下是计算电流 -->
	    <view class="info">
	      <text class="txt txtbiaoti">电压（U）</text>
	      <view style="display: flex;justify-content: flex-end;">
	        <input class="inp" type="digit" maxlength=10 placeholder="请输入电压值" v-model="UInput" style="height: 65rpx;"/>
	        <text class="txt txtdanwei">kV</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti">电容（C）</text>
	      <view style="display: flex;justify-content: flex-end;">
	        <input class="inp" type="digit" maxlength=10 placeholder="请输入电容" v-model="CInput" style="height: 65rpx;"/>
	        <text class="txt txtdanwei">μF</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti">频率（F）</text>
	      <view style="display: flex;justify-content: flex-end;">
	        <input class="inp" type="digit" maxlength=10 placeholder="请输入频率" v-model="FInput" style="height: 65rpx;"/>
	        <text class="txt txtdanwei">Hz</text>
	      </view>
	    </view>
	    <view class="info" style="border: 2rpx solid red;">
	      <text class="txt txtbiaoti" style="color: red;">电流（I）</text>
	      <view style="display: flex;justify-content: flex-end;">
	        <input class="inp" type="digit" maxlength=10 placeholder="点击计算查看结果" disabled placeholder-style="color:red;" style="color:red;height: 65rpx;"  v-model="IInput" />
	        <text class="txt txtdanwei" style="color: red;">A&nbsp;</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtgongshi">计算公式：I=2π*F*U*C</text>
	    </view>
	    <view style="display: flex;align-items: center;justify-content: center;">
	      <button class="but1" @click="calculateI">立即计算</button>
	      <button class="but2" @click="clearInputs1">全部清空</button>
	    </view>
	  </view>
	  
	  <view v-if="tab2 === 'qqq'" class="con1">      <!-- 以下是计算品质因数 -->
	    <view class="info">
	      <text class="txt txtbiaoti">电感（L）</text>
	      <view style="display: flex;justify-content: flex-end;">
	        <input class="inp" type="digit" maxlength=10 placeholder="请输入电感" v-model="LInput" style="height: 65rpx;"/>
	        <text class="txt txtdanwei">H&nbsp;</text>
	      </view>
	    </view>
	    <view class="info">
	      <text class="txt txtbiaoti">电容（C）</text>
	      <view style="display: flex;justify-content: flex-end;">
	        <input class="inp" type="digit" maxlength=10 placeholder="请输入电容" v-model="CInput" style="height: 65rpx;"/>
	        <text class="txt txtdanwei">μF</text>
	      </view>
	    </view>
		<view class="info">
		  <text class="txt txtbiaoti">电阻（R）</text>
		  <view style="display: flex;justify-content: flex-end;">
		    <input class="inp" type="digit" maxlength=10 placeholder="请输入电阻" v-model="RInput" style="height: 65rpx;"/>
		    <text class="txt txtdanwei">Ω&nbsp;</text>
		  </view>
		</view>
		<view class="info" style="border: 2rpx solid red;">
		  <text class="txt txtbiaoti" style="color: red;">因数（Q）</text>
		  <view style="display: flex;justify-content: flex-end;">
		    <input class="inp" type="digit" maxlength=10 placeholder="点击计算查看结果" disabled placeholder-style="color:red;" style="color:red;height: 65rpx;"  v-model="QInput" />
		    <text class="txt txtdanwei" style="color: red;">&nbsp;&nbsp;</text>
		  </view>
		</view>
		<view class="info">
		  <text class="txt txtgongshi">计算公式：Q=1/R*(L/C)^(1/2)</text>
		</view>
		<view style="display: flex;align-items: center;justify-content: center;">
		  <button class="but1" @click="calculateQ">立即计算</button>
		  <button class="but2" @click="clearInputs1">全部清空</button>
		</view>
	  </view>
	</view>
  </view>
</template>

<script>
import { shareMixin } from '/shareMixin.js';
export default {
  mixins: [shareMixin],
  data() {
    return {
	  shareTitle: '电气试验宝典-串谐在线计算工具', // 设置自定义的分享标题
      tab1: 'F', 
	  tab2:'dianliu',// 当前选中的选项卡
      CInput: null, // 电容输入值
      LInput: null, // 电感输入值
      FInput: null, // 频率输入值
      popupMessage: '', // 弹窗提示信息
      UInput: null, // 电压输入值
      IInput: null ,// 电流输入值
	  RInput: null ,
	  QInput: null , //品质因数输入值
    };
  },
  methods: {
    // 计算频率的方法
    calculateF() {
      const L = this.LInput;
      const C = this.CInput;
      if (L && C) {
        // 计算频率，公式为 F = 1 / (2π√(LC))
        const F = 1 / (2 * Math.PI * Math.sqrt(L * C * 1e-6));
        this.FInput = F.toFixed(4); // 保留四位小数
      } else {
        // 如果电感或电容未输入，设置提示信息并打开弹窗
        this.popupMessage = '请正确输入电感和电容！';
        this.$refs.popup.open();
      }
    },
    
    // 计算电流的方法
    calculateI() {
      const U = this.UInput;
      const C = this.CInput;
      const F = this.FInput;
      if (U && C && F) {
        // 计算电流，公式为 I = 2π * F * U * C
        const I = 2 * Math.PI * F * U * C * 1e-3;
        this.IInput = I.toFixed(4); // 保留四位小数
      } else {
        // 如果电压值、电容或频率未输入，设置提示信息并打开弹窗
        this.popupMessage = '请正确输入电压、电容和频率！';
        this.$refs.popup.open();
      }
    },
    
    // 计算电容的方法
    calculateC() {
      const L = this.LInput;
      const F = this.FInput;
      if (L && F) {
        // 计算电容，公式为 C = 1 / ((2πF)²L)
        const C = 1 / ((2 * Math.PI * F) ** 2 * L) * 1e6;
        this.CInput = C.toFixed(4); // 保留四位小数
        console.log('计算出的电容为:', C);
      } else {
        // 如果电感或频率未输入，设置提示信息并打开弹窗
        this.popupMessage = '请正确输入电感和频率值！';
        this.$refs.popup.open();
      }
    },
    
    // 计算电感的方法
    calculateL() {
      const C = this.CInput;
      const F = this.FInput;
      if (C && F) {
        // 计算电感，公式为 L = 1 / ((2πF)²C)
        const L = 1 / ((2 * Math.PI * F) ** 2 * C) * 1e6;
        this.LInput = L.toFixed(4); // 保留四位小数
        console.log('计算出的电感为:', L);
      } else {
        // 如果电容或频率未输入，设置提示信息并打开弹窗
        this.popupMessage = '请正确输入电容和频率值！';
        this.$refs.popup.open();
      }
    },
	
	// 计算品质因数的方法
	calculateQ() {
	  const induct = this.LInput;
	  const C = this.CInput;
	  const R = this.RInput;
	  if (induct && C && R) {
	    // 计算电流，公式为 I = 2π * F * U * C
	    const Q = 1 / R * Math.sqrt(induct / C) * 1e3;
	    this.QInput = Q.toFixed(4); // 保留四位小数
	  } else {
	    // 如果电压值、电容或频率未输入，设置提示信息并打开弹窗
	    this.popupMessage = '请正确输入电感、电容和电阻！';
	    this.$refs.popup.open();
	  }
	},
    
    // 清空所有输入的方法
    clearInputs1() {
      this.CInput = null;
      this.LInput = null;
      this.FInput = null;
      this.UInput = null;
	  this.IInput = null;
	  this.QInput = null;
	  this.RInput = null;
    },
	clearInputs2() {
	  this.CInput = null;
	  this.LInput = null;
	  this.FInput = null;
	  
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
  margin: 0rpx 7rpx 20rpx 10rpx;
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
  border: 2rpx  solid #3c9cff;
}
.info {
  display: flex;
  height:auto;
  font-size: 36rpx;
  justify-content: space-between;
  padding: 0;     /* 10rpx 20rpx 10rpx 20rpx*/
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
.txt{
	display: flex;
	align-items: center;
	justify-content: center;
	height: 65rpx;
	padding:1rpx 10rpx 1rpx 10rpx ;
}
.txtbiaoti{
	font-size: 34rpx;
	background-color: #ecf5ff;
	border-radius: 30rpx 0 0 30rpx;
	width: 220rpx;
}
.txtgongshi{
	font-size: 34rpx;
	width: auto;
	margin-left: 10rpx;
}
.txtdanwei{
	font-weight: bold;
	font-size: 32rpx;
}
.but1{
	margin-bottom:20rpx; 
	background-color: rgb(58, 185, 158);
	height: 90rpx;
	width: 240rpx;
	font-size: 36rpx;
}
.but2{
	margin-bottom:20rpx; 
	background-color: #e45656;
	height: 90rpx;
	width: 240rpx;
	font-size: 36rpx;
}
.but1:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
.but2:active {
		  transform: scale(0.96);  
		  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.1);
		  }
</style>