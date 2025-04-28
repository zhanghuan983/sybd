<template>
  <view class="content">
    <view
      style="height: auto; background: #ecf5ff; color: #909193; display: flex; flex-direction: column; padding: 5rpx 10rpx;"
    >
	  <view style="width: 730rpx; font-size: 30rpx; font-weight: bold;">5.1 同步发电机和调相机</view>
      <text style="font-size: 28rpx;">容量为6000kW及以上的同步发电机、调相机的试验项目、周期和要求见下，6000kW以下者可参照执行。</text>
    </view>

    <uv-vtabs
      :chain="chain"
      :list="list"
      :height="height"
      hdHeight="100rpx"
	  barWidth="200rpx"
      @change="change"
      @scrolltolower="scrolltolower"
    >
      <!-- 第一个选项卡 -->
      <uv-vtabs-item index="0">
        <view class="item1">
          <view class="item-title">
            <text class="text">定子绝缘电阻、吸收比或极化指数</text>
          </view>
          <view class="item-content">
            <view class="text">
              <!-- 修改这里的 @click 事件绑定 -->
              <uv-tabs :list="list1" @click="handleClick1" ></uv-tabs>
              <text>{{ textToDisplay1 }}</text>
            </view>
          </view>
        </view>
        <view class="gap">
          <uv-gap bg-color="#f1f1f1" height="4"></uv-gap>
        </view>
      </uv-vtabs-item>

      <!-- 第二个选项卡 -->
      <uv-vtabs-item index="1">
        <view class="item1">
          <view class="item-title">
            <text class="text">定子绕组直流电阻</text>
          </view>
          <view class="item-content">
            <view class="text">
              <!-- 修改这里的 @click 事件绑定 -->
              <uv-tabs :list="list2" @click="handleClick2"></uv-tabs>
              <text>{{ textToDisplay2 }}</text>
            </view>
          </view>
        </view>
        <view class="gap">
          <uv-gap bg-color="#f1f1f1" height="4"></uv-gap>
        </view>
      </uv-vtabs-item>

      <!-- 第三个选项卡 -->
      <uv-vtabs-item index="2">
        <view class="item1">
          <view class="item-title">
            <text class="text">定子绕组泄漏电流和直流耐压</text>
          </view>
          <view class="item-content">
            <view class="text">
              <!-- 修改这里的 @click 事件绑定 -->
              <uv-tabs :list="list3" @click="handleClick3"></uv-tabs>
              <text>{{ textToDisplay3 }}</text>
            </view>
          </view>
        </view>
        <view class="gap">
          <uv-gap bg-color="#f1f1f1" height="4"></uv-gap>
        </view>
      </uv-vtabs-item>

      <!-- 第四个选项卡 -->
      <uv-vtabs-item index="3">
        <view class="item1">
          <view class="item-title">
            <text class="text">主题扩展</text>
          </view>
          <view class="item-content">
            <text class="text">
              uv-ui中的uv-ui-tools组件下面的theme.scss为主题文件，直接在uni.scss中引入主题即可，可以根据自己的需求进行扩展。下面也有说明具体使用方式。使用方法请参考：
            </text>
          </view>
        </view>
        <view class="gap">
          <uv-gap bg-color="#f1f1f1" height="4"></uv-gap>
        </view>
      </uv-vtabs-item>

      <!-- 第五个选项卡 -->
      <uv-vtabs-item index="4">
        <view class="item1">
          <view class="item-title">
            <text class="text">更新日志</text>
          </view>
          <view class="item-content">
            <text class="text">
              uv-ui的重大更新在更新日志中都有所说明，如果在开发的过程中遇到文档不完善，可以提供给我们，我们会持续完善，非常感谢大家的支持。更新日志：
            </text>
          </view>
        </view>
        <view class="gap">
          <uv-gap bg-color="#f1f1f1" height="4"></uv-gap>
        </view>
      </uv-vtabs-item>

      <!-- 第六个选项卡 -->
      <uv-vtabs-item index="5">
        <view class="item1">
          <view class="item-title">
            <text class="text">设计规范</text>
          </view>
          <view class="item-content">
            <text class="text">
              为了约束合成更多优秀的组件和模板，打造优质的体验，我们拟定了一些UI界面设计和建议。同时部分之间会有依赖，这是为了减少代码冗余的同时提高开发效率，模块化是我们的基础。如果大家有好的建议，可以提出进行改进。
            </text>
          </view>
        </view>
        <view class="gap">
          <uv-gap bg-color="#f1f1f1" height="4"></uv-gap>
        </view>
      </uv-vtabs-item>

      <!-- 第七个选项卡 -->
      <uv-vtabs-item index="6">
        <view class="item1">
          <view class="item-title">
            <text class="text">交流反馈</text>
          </view>
          <view class="item-content">
            <text class="text">
              为采用MIT许可证的开源项目，使用完全免费。欢迎加QQ群交流反馈，一起学习，共同进步。
            </text>
          </view>
        </view>
        <view class="gap">
          <uv-gap bg-color="#f1f1f1" height="4"></uv-gap>
        </view>
      </uv-vtabs-item>

      <!-- 可选：添加一个高度为600的间隙 -->
      <uv-gap bg-color="#fff" height="600"></uv-gap>
    </uv-vtabs>
  </view>
</template>

<script>
export default {
  data() {
    return {
	  list1: [{
			  name: '周期',
			  }, {
			  name: '判据',
			  }, {
			  name: '方法及说明'
			  }],
	  list2: [{
	  		  name: '周期',
	  		  }, {
	  		  name: '判据',
	  		  }, {
	  		  name: '方法及说明'
	  		  }],
	  list3: [{
	  		  name: '周期',
	  		  }, {
	  		  name: '判据',
	  		  }, {
	  		  name: '方法及说明'
	  		  }],
      list: [
        { name: '定子绝缘电阻', badge: { show: false } },
        { name: '定子直流电阻', badge: { show: false } },
        { name: '定子直流耐压', badge: { show: false } },
        { name: '定子工频耐压', badge: { show: false } },
        { name: '更新日志', badge: { show: false } },
        { name: '设计规范', badge: { show: false } },
        { name: '交流反馈', badge: { show: false } }
      ],
      chain: true,     //  是否联动
	  showText: false, // 控制显示文本的开关
	  textToDisplay1: '点击上面标签，查看内容', // 打开页面默认加载内容
	  textToDisplay2: '点击上面标签，查看内容',
	  textToDisplay3: '点击上面标签，查看内容',
    };
  },
  computed: {
    height() {
      return uni.getSystemInfoSync().windowHeight - uni.upx2px(100);
    }
    // 如果需要动态设置高度，可以保留这个计算属性
  },
  onReady() {
    // 如果不需要模拟接口请求，可以移除以下代码
    // uni.showLoading({
    //   title: '加载中'
    // });
    // setTimeout(() => {
    //   this.list = getList;
    //   uni.hideLoading();
    // }, 500);
  },
  methods: {
    change(index) {
      console.log('选项改变：', index);
    },
    scrolltolower(index) {
      console.log('内容滚动到底部触发：', index);
    },
	handleClick1(item) {
	  console.log('item', item);
	  if (item.name === '周期') {
	    this.textToDisplay1 = '1）C级检修时\n2）A级检修前、后\n3）必要时';
	  } else if (item.name === '判据') {
	    this.textToDisplay1 = '1）绝缘电阻值自行规定，可参照产品技术文件要求或GB/T20160；\n2）各相或分支绝缘电阻值的差值不应大于最小值的100%；\n3）吸收比或极化指数：环氧粉云母绝缘吸收比不应小于1.6或极化指数不应小于2.0；其它绝缘材料参照产品技术文件要求；\n4）对汇水管死接地的电机宜在无水情况下进行,在有水情况下应符合产品技术文件要求;对汇水管非死接地的电机，测量时应消除水的影响。';
	  } else if (item.name === '方法及说明') {
		this.textToDisplay1 = '1）额定电压为1000V以上者，采用2500V绝缘电阻测试仪；额定电压为20000V及以上者，可采用5000V绝缘电阻测试仪，量程不宜低于10000MΩ；2）水内冷发电机汇水管有绝缘者应使用专用绝缘电阻测试仪，汇水管对地电阻及对绕组电阻应满足专用绝缘电阻测试仪使用条件，汇水管对地电阻可以用数字万用表测量；3）200MW及以上机组推荐测量极化指数。';
	  } else {
	    this.textToDisplay1 = '加载错误，请重试';
	  }
	  this.showText = this.textToDisplay1 !== '';
	},
	handleClick2(item) {
	  console.log('item', item);
	  if (item.name === '周期') {
	    this.textToDisplay2 = '1）不超过3年\n2）A级检修时\n3）必要时';
	  } else if (item.name === '判据') {
	    this.textToDisplay2 = '各相或各分支的直流电阻值,在校正了由于引线长度不同而引起的误差后，相互之间的差别不得大于最小值的2%。换算至相同温度下初值比较,相差不得大于最小值的2%。超出此限值者，应查明原因。';
	  } else if (item.name === '方法及说明') {
		this.textToDisplay2 = '1）在冷态下测量时，绕组表面温度与周围空气温度之差不应大于±3℃；\n2）相间（或分支间）差别及其历年的相对变化大于1%时，应引起注意；\n3）分支数较多的水轮发电机组可在A、B级检修及必要时时测量。';
	  } else {
	    this.textToDisplay2 = '加载错误，请重试';
	  }
	  this.showText = this.textToDisplay2 !== '';
	},
	handleClick3(item) {
	  console.log('item', item);
	  if (item.name === '周期') {
	    this.textToDisplay3 = '1）不超过3年\n2）A级检修前、后\n3）更换绕组后\n4）必要时';
	  } else if (item.name === '判据') {
	    this.textToDisplay3 = '1）额定电压为27000V及以下的电机试验电压如下：\n  a)全部更换定子绕组并修好后的试验电压为3.0Uɴ；\nb)局部更换定子绕组并修好后的试验电压为2.5Uɴ；\nc)A级检修前且运行20年及以下者的试验电压为2.5Uɴ；\nd)A级检修前且运行20年以上与架空线直接连接者的试验电压为2.5Uɴ；\ne)A级检修前且运行20年以上不与架空线直接连接者的试验电压为(2.0〜2.5)Uɴ；\nf)A级检修后或其它检修时的试验电压为2.0Uɴ。\n2）在规定的试验电压下，各相泄漏电流之间的差别不应大于最小值的100%；最大泄漏电流在20μA以下者，可不考虑各相泄漏电流之间的差别；\n3）泄漏电流不随时间的延长而增大。';
	  } else if (item.name === '方法及说明') {
		this.textToDisplay3 = '1）检修前试验，应在停机后清除污秽前，尽量在热态下进行。氢冷发电机在充氢条件下试验时，氢纯度应在96%以上，严禁在置换过程中进行试验；\n2）试验电压按每级0.5A分阶段升高，每阶段停留1min；\n3）不符合2）、3）要求之一者，应尽可能找出原因并消除，但并非不能运行；\n4）泄漏电流随电压不成比例显著增长时，应注意分析；\n5）试验应采用高压屏蔽法接线，微安表接在高压侧；必要时可对出线套管表面加以屏蔽。水内冷发电机汇水管有绝缘者，应采用低压屏蔽法接线；汇水管死接地者，应尽可能在不通水和引水管吹净条件下进行试验。冷却水质应满足产品技术文件要求，如有必要，应尽量降低内冷水电导率；6）对汇水管直接接地的发电机在不具备做直流泄漏试验的条件下，可在通水条件下进行直流耐压试验，总电流不应突变。';
	  } else {
	    this.textToDisplay3 = '加载错误，请重试';
	  }
	  this.showText = this.textToDisplay3 !== '';
	},
  }
};
</script>

<style scoped>
.content {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.item1 {
  padding: 10rpx;
}
.item-title {
  font-size: 30rpx;
  font-weight: bold;
  margin-bottom: 0rpx;
}
.item-content {
  font-size: 30rpx;
  color: #666;
}
.gap {
  padding: 5rpx 0;
}
</style>