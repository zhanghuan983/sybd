<template>
  <view class="container">
    <input type="number" v-model="inputValue1" placeholder="请输入第一个值" />
    <input type="number" v-model="inputValue2" placeholder="请输入第二个值" />
    <input type="number" v-model="inputValue3" placeholder="请输入第三个值" />
    <button @click="calculateProduct">计算乘积</button>
    <view class="result">计算结果: {{ result }}</view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      inputValue1: '',
      inputValue2: '',
      inputValue3: '',
      result: '',
    };
  },
  methods: {
    calculateProduct() {
      const num1 = parseFloat(this.inputValue1);
      const num2 = parseFloat(this.inputValue2);
      const num3 = parseFloat(this.inputValue3);
      if (!isNaN(num1) &&!isNaN(num2) &&!isNaN(num3)) {
        this.result = num1 * num2 * num3;
      } else {
        uni.showToast({
          title: '请输入正确的数字',
          icon: 'none',
        });
      }
    },
  },
  onShareAppMessage() {
    return {
      title: '分享乘积计算页面',
      path: `/pages/biaozhun/fenxiang?input1=${this.inputValue1}&input2=${this.inputValue2}&input3=${this.inputValue3}&result=${this.result}`,
    };
  },
  onLoad(options) {
    if (options.input1 && options.input2 && options.input3 && options.result) {
      this.inputValue1 = options.input1;
      this.inputValue2 = options.input2;
      this.inputValue3 = options.input3;
      this.result = options.result;
    }
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
input {
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 80%;
  margin-bottom: 10px;
  padding: 5px;
}
button {
  background-color: #007aff;
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px 20px;
  margin-bottom: 10px;
}
.result {
  font-size: 16px;
}
</style>