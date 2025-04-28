<template>
	<view class="content">
		<view
		  style="height: auto; background: #ecf5ff; color: #909193; display: flex; flex-direction: column; padding: 5rpx 10rpx;"
		>
		  <view style="width: 730rpx; font-size: 34rpx; font-weight: bold;">6.1 油浸式电力变压器</view>
		  <text style="font-size: 32rpx;">油浸式电力变压器的试验项目、周期和要求见下。</text>
		</view>
		<uv-vtabs 
			:chain="chain"
			:list="list"
			:barItemBadgeStyle="{right:'2rpx',top:'2rpx',size:'2rpx'}"
			barWidth=150rpx
			@change="change"
			:bar-item-active-line-style="{background: '#2878FF'}"
			>
			<uv-vtabs-item>
				<view 
					class="item"
					v-for="(item2,index2) in list2"
					:key="index2">
					<view class="item-title">
						<text class="text">{{item2.name}}</text>
					</view>
					<view class="item-content">
						<view  v-if="item2.name === '红外测温'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick2"></uv-tabs>
							<text class="txt">{{ textToDisplay2 }}</text>
						</view>
						<view  v-if="item2.name === '油中溶解气体分析'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick3"></uv-tabs>
							<text class="txt">{{ textToDisplay3 }}</text>
						</view>
						<view  v-if="item2.name === '绝缘油试验'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick4"></uv-tabs>
							<text class="txt">{{ textToDisplay4 }}</text>
						</view>
						<view  v-if="item2.name === '定子绕组工频交流耐压'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick5"></uv-tabs>
							<text class="txt">{{ textToDisplay5 }}</text>
						</view>
						<view  v-if="item2.name === '转子绕组绝缘电阻'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick6"></uv-tabs>
							<text class="txt">{{ textToDisplay6 }}</text>
						</view>
						<view  v-if="item2.name === '转子绕组直流电阻'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick7"></uv-tabs>
							<text class="txt">{{ textToDisplay7 }}</text>
						</view>
						<view  v-if="item2.name === '转子绕组交流耐压'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick8"></uv-tabs>
							<text class="txt">{{ textToDisplay8 }}</text>
						</view>
						<view  v-if="item2.name === '发电机和励磁机的励磁回路所连接设备(不包括发电机转子和励磁机电枢)的绝缘电阻'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick9"></uv-tabs>
							<text class="txt">{{ textToDisplay9 }}</text>
						</view>
						<view  v-if="item2.name === '发电机和励磁机的励磁回路所连接设备(不包括发电机转子和励磁机电枢)交流耐压'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick10"></uv-tabs>
							<text class="txt">{{ textToDisplay10 }}</text>
						</view>
						<view  v-if="item2.name === '定子铁心磁化试验GB20835'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick11"></uv-tabs>
							<text class="txt">{{ textToDisplay11 }}</text>
						</view>
						<view  v-if="item2.name === '发电机和励磁机轴承绝缘电阻'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick12"></uv-tabs>
							<text class="txt">{{ textToDisplay12 }}</text>
						</view>
						<view  v-if="item2.name === '灭磁电阻器(或自同期电阻器)直流电阻'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick13"></uv-tabs>
							<text class="txt">{{ textToDisplay13 }}</text>
						</view>
						<view  v-if="item2.name === '灭磁开关并联电阻'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick14"></uv-tabs>
							<text class="txt">{{ textToDisplay14 }}</text>
						</view>
						<view  v-if="item2.name === '转子绕组的交流阻抗和功率损耗'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick15"></uv-tabs>
							<text class="txt">{{ textToDisplay15 }}</text>
						</view>
						<view  v-if="item2.name === '重复脉冲(RSO)法测量转子匝间短路'">
							<uv-tabs lineHeight="5" :list="list12" @click="handleClick16"></uv-tabs>
							<text class="txt">{{ textToDisplay16 }}</text>
						</view>
					</view>
				</view>
			</uv-vtabs-item>
		</uv-vtabs>
	</view>
</template>

<script>
	const getList = [{
		name: '红外测温',
		badge: {
					
				},
		childrens: [{
			name: '红外测温',
		}]
	}, {
		name: '油中溶解气体分析',
		badge: {
					
				},
		childrens: [{
			name: '油中溶解气体分析',
		}, ]
	}, {
		name: '绝缘油试验',
		badge: {
					
				},
		childrens: [{
			name: '绝缘油试验',
		}]
	}, {
		name: '定子绕组交流耐压',
		badge: {
					isDot: true
				},
		childrens: [{
			name: '定子绕组工频交流耐压',
		}]
	}, {
		name: '转子绕组绝缘电阻',
		badge: {
					isDot: true
				},
		childrens: [{
			name: '转子绕组绝缘电阻',
		}]
	},{
		name: '转子绕组直流电阻',
		badge: {
					isDot: true
				},
		childrens: [{
			name: '转子绕组直流电阻',
		}]
	},{
		name: '转子绕组交流耐压',
		childrens: [{
			name: '转子绕组交流耐压',
		}]
	},{
		name: '励磁回路绝缘电阻',
		childrens: [{
			name: '发电机和励磁机的励磁回路所连接设备(不包括发电机转子和励磁机电枢)的绝缘电阻',
		}]
	},{
		name: '励磁回路交流耐压',
		childrens: [{
			name: '发电机和励磁机的励磁回路所连接设备(不包括发电机转子和励磁机电枢)交流耐压',
		}]
	},{
		name: '定子铁心磁化试验',
		childrens: [{
			name: '定子铁心磁化试验GB20835',
		}]
	},{
		name: '励磁机轴承绝缘',
		childrens: [{
			name: '发电机和励磁机轴承绝缘电阻',
		}]
	},{
		name: '灭磁电阻器直阻',
		childrens: [{
			name: '灭磁电阻器(或自同期电阻器)直流电阻',
		}]
	},{
		name: '灭磁开关并联电阻',
		childrens: [{
			name: '灭磁开关并联电阻',
		}]
	},{
		name: '转子交流阻抗和功率损耗',
		childrens: [{
			name: '转子绕组的交流阻抗和功率损耗',
		}]
	},{
		name: '转子匝间短路(RSO)测量',
		childrens: [{
			name: '重复脉冲(RSO)法测量转子匝间短路',
		}]
	}]
	export default {
		data() {
			return {
				list: [],
				chain: false,
				value: 0,
				list12: [{
						  name: '周期',
						  }, {
						  name: '判据',
						  }, {
						  name: '方法及说明'
						  }],
				textToDisplay2: '点击上方标签，查看相应内容',
				textToDisplay3: '点击上方标签，查看相应内容',
				textToDisplay4: '点击上方标签，查看相应内容',
				textToDisplay5: '点击上方标签，查看相应内容',
				textToDisplay6: '点击上方标签，查看相应内容',
				textToDisplay7: '点击上方标签，查看相应内容',
				textToDisplay8: '点击上方标签，查看相应内容',
				textToDisplay9: '点击上方标签，查看相应内容',
				textToDisplay10: '点击上方标签，查看相应内容',
				textToDisplay11: '点击上方标签，查看相应内容',
				textToDisplay12: '点击上方标签，查看相应内容',
				textToDisplay13: '点击上方标签，查看相应内容',
				textToDisplay14: '点击上方标签，查看相应内容',
				textToDisplay15: '点击上方标签，查看相应内容',
				textToDisplay16: '点击上方标签，查看相应内容',
			}
		},
		computed: {
			list2() {
				const _list = this.list[this.value]?.childrens;
				return _list ? _list : [];
			}
		},
		onReady() {
			// 模拟接口请求数据
			uni.showLoading({
				title: '加载中'
			})
			setTimeout(() => {
				this.list = getList;
				uni.hideLoading();
			}, 200)
		},
		methods: {
			change(index) {
				console.log('选项改变：',index)
				this.value = index;
			},
			handleClick2(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay2 = '1)>330kV：1个月\n2)220kV：3个月\n3)<110kV：6个月\n4)必要时';
			  } else if (item.name === '判据') {
			    this.textToDisplay2 = '各部位无异常温升现象，检测和分析方法参考DL/T 664。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay2 = '无';
			  } else {
			    this.textToDisplay2 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay2 !== '';
			},
			handleClick3(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay3 = '1）A、B级检修后，66kV及以上：1,4,10,30天;\n2）运行中电网侧：750kV：1个月；330kV~500kV：3个月；220kV：6个月；35kV~110kV：1年。\n3）运行中发电侧：120MVA及以上的发电厂主变压器为6个月；8MVA及以上的变压器为1年；8MVA以下的油浸式变压器自行规定；\n4）必要时。';
			  } else if (item.name === '判据') {
			    this.textToDisplay3 = '按DL/T 722判断是否符合要求：1）新装变压器油中H2与烃类气体含量（μL/L）任一项不宜超过下列数值：500kV及以上：总烃：10；H2：10；C2H2：0.1；330kV及以下：总烃：20；H2：30；C2H2：0.1。\n2）运行变压器油中H2与烃类气体含量（μL/L）超过下列任何一项值时应引起注意：总烃:150；H2：150；C2H2：5（35kV〜220kV）,1（330kV及以上）。\n3）烃类气体总和的产气速率大于6mL/d（开放式）和12mL/d（密封式），或相对产气速率大于10%/月则认为设备有异常（对乙炔＜（μL/L、总烃小于新设备投运要求时，总烃的绝对产气率可不作分析）。氢气的产气速率大于5mL/d（开放式）和10mL/d（密封式），则认为设备有异常。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay3 = '按DL/T 722取样及测量：\n1）总烃包括CH4、C2H4、C2H6和C2H2四种气体；\n2）溶解气体组份含量有增长趋势时，可结合产气速率判断，必要时缩短周期进行跟踪分析；\n3）总烃含量低的设备不宜采用相对产气速率进行判断；';
			  } else {
			    this.textToDisplay3 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay3 !== '';
			},
			handleClick4(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay4 = '见第15章表48。';
			  } else if (item.name === '判据') {
			    this.textToDisplay4 = '见第15章表48。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay4 = '见第15章表48。';
			  } else {
			    this.textToDisplay4 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay4 !== '';
			},
			handleClick5(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay5 = '1）A级检修前\n2）更换绕组后';
			  } else if (item.name === '判据') {
			    this.textToDisplay5 = '1）全部更换定子绕组并修好后的电机，试验电压如下：\na）对于容量小于10MVA且额定电压不低于380V的者，其试验电压为2Un+1000,但最低为1500V；\nb）对于容量大于等于10MVA者，当其额定电压为6kV时，试验电压为2.5Un；当其额定电压大于等于6kV且不大于24kV时,试验电压为2Un+1000；当其额定电压大于24kV时，试验电压为2Un+1000，或按设备供货协议执行。\n2）A级检修前或局部更换定子绕组并修好后的电机，试验电压为：\na）对于运行20年及以下者，试验电压为1.5Un；\nb）对于运行20年以上与架空线路直接连接者，试验电压为1.5Un；\nc）对于运行20年以上不与架空线路直接连接者，试验电压为（1.3〜1.5）Un。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay5 = '1）检修前的试验，应在停机后清除污秽前，尽可能在热态下进行。处于备用状态时，可在冷状态下进行。氢冷发电机在充氢条件下试验时，氢纯度应在96%以上，严禁在置换过程中进行试验；\n2）水内冷电机宜在通水的情况下进行试验，冷却水质应满足制造厂技术说明书中相应要求；\n3）在采用变频谐振耐压时，试验频率应在45〜55Hz范围内；\n4）全部或局部更换定子绕组的工艺过程中的试验电压见附录A、B；\n5）如采用超低频（0.1Hz）耐压，试验电压峰值为工频试验电压峰值的1.2倍。';
			  } else {
			    this.textToDisplay5 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay5 !== '';
			},
			handleClick6(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay6 = '1）B、C级检修时\n2）A级检修中转子清扫前、后\n3）必要时';
			  } else if (item.name === '判据') {
			    this.textToDisplay6 = '1）绝缘电阻值不宜小于0.5MΩ；\n2）水内冷转子绕组绝缘电阻值不宜小于5kΩ。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay6 = '1）采用1000V绝缘电阻测试仪测量。转子水内冷发电机用250〜500V绝缘电阻测试仪；\n2）对于300MW以下的隐极式电机，当转子绕组未干燥完毕时，如果转子绕组的绝缘电阻值在75℃时不小于2kΩ，或在20℃时不小于20kΩ，在排除转子绕组有接地的前提下，允许转子绕组投入运行；\n3）对于300MW及以上的隐极式电机，转子绕组的绝缘电阻值在10〜30℃时不小于0.5MΩ。';
			  } else {
			    this.textToDisplay6 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay6 !== '';
			},
			handleClick7(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay7 = '1）A级检修时\n2）必要时';
			  } else if (item.name === '判据') {
			    this.textToDisplay7 = '与初值比较，换算至同一温度下其差别不宜超过2%。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay7 = '1）在冷态下进行测量；\n2）显极式转子绕组还应对各磁极线圈间的连接点进行测量；\n3）对于频繁启动的燃气轮机发电机，应在A、B、C级检修时测量不同角度的转子绕组直流电阻。';
			  } else {
			    this.textToDisplay7 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay7 !== '';
			},
			handleClick8(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay8 = '1）凸极式转子A级检修时和更换绕组后\n2）隐极式转子拆卸护环后，局部修理槽内绝缘和更换绕组后';
			  } else if (item.name === '判据') {
			    this.textToDisplay8 = '1）对于凸极式和隐极式转子全部更换绕组并修好后的电机，当其额定励磁电压为500V及以下者，试验电压为10Un,但不低于1500V；当其额定励磁电压为500V以上者，试验电压为2Un+4000V；\n2）对于凸极式转子A级检修时及局部更换绕组并修好后的电机,试验电压为5Un，但不低于1000V，不大于2000V；\n3)对于隐极式转子局部修理槽内绝缘后及局部更换绕组并修好后的电机，试验电压为5Un，但不低于1000V, 不大于2000V。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay8 = '1）隐极式转子拆卸护环只修理端部绝缘时，可用2500V绝缘电阻测试仪测绝缘电阻代替；\n2）同步发电机转子绕组全部更换绝缘时的交流试验电压按产品技术文件要求执行。';
			  } else {
			    this.textToDisplay8 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay8 !== '';
			},
			handleClick9(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay9 = '1）A、B、C级检修时\n2）必要时';
			  } else if (item.name === '判据') {
			    this.textToDisplay9 = '绝缘电阻值不应低于0.5MΩ，否则应查明原因并消除。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay9 = '1）A级检修时用2500V绝缘电阻测试仪；\n2）B、C级检修时用1000V绝缘电阻测试仪。';
			  } else {
			    this.textToDisplay9 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay9 !== '';
			},
			handleClick10(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay10 = 'A级检修时';
			  } else if (item.name === '判据') {
			    this.textToDisplay10 = '试验电压为1000V。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay10 = '可用2500V绝缘电阻测试仪测绝缘电阻代替。';
			  } else {
			    this.textToDisplay10 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay10 !== '';
			},
			handleClick11(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay11 = '1）重新组装或更换、修理硅钢片后\n2）必要时';
			  } else if (item.name === '判据') {
			    this.textToDisplay11 = '1）折算至规定的磁密和时间下，铁心相同部位（齿或槽）的最高温升不应大于25K、最大温差不应大于15K；\n2）对运行年久的电机，应根据历史数据自行规定。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay11 = '1）水轮发电机的磁通密度应为1.OT,不宜低于0.9T；汽轮发电机的磁通密度应在1.4T，不宜低于1.26T，在磁密为1.4T下持续时间为45min。当试验时的磁密与要求的磁密不相等时，应改变试验持续时间，持续试验时间与磁密折算方法见附录C.l。对直径较大的水轮发电机试验时应注意校正由于磁通密度分布不均匀所引起的误差；\n2）受现场条件限制时，在磁密为1T下持续试验时间为90min；\n3）铁心磁化试验比损耗及试验数据修正折算方法见附录C；\n4）采用红外成像仪进行温度测量；\n5）定子铁心初始温度和环境温度温差应不超过5K；\n6）对于铁心局部故障修理后或者需查找铁心局部缺陷的电机，可使用电磁式定子铁心检测仪通小电流法对铁心局部进行检测，推荐判定标准参见附录D，但最终判断依据为全磁通方法。';
			  } else {
			    this.textToDisplay11 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay11 !== '';
			},
			handleClick12(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay12 = 'A级检修时';
			  } else if (item.name === '判据') {
			    this.textToDisplay12 = '1）汽轮发电机组的轴承不得低于0.5MΩ；\n2）立式水轮发电机组的推力轴承每一轴瓦不应低于100MΩ；油槽充油并顶起转子时，不应低于0.3MΩ；轴瓴绝缘的水轮发电机上端轴瓴采用250V绝缘电阻测试仪测量时，不应低于1MΩ；\n3）所有类型的水轮发电机，凡有绝缘的导轴承，油槽充油前，每一轴瓦不应低于100MΩ。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay12 = '汽轮发电机组的轴承绝缘，用1000V绝缘电阻测试仪在安装好油管后进行测量。';
			  } else {
			    this.textToDisplay12 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay12 !== '';
			},
			handleClick13(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay13 = 'A级检修时';
			  } else if (item.name === '判据') {
			    this.textToDisplay13 = '线性电阻与铭牌或最初测得的数据比较，其差别不应超过10%。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay13 = '非线性电阻遵照产品技术文件要求执行。';
			  } else {
			    this.textToDisplay13 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay13 !== '';
			},
			handleClick14(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay14 = 'A级检修时';
			  } else if (item.name === '判据') {
			    this.textToDisplay14 = '与初值比较应无显著差别。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay14 = '电阻值应分段测量。';
			  } else {
			    this.textToDisplay14 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay14 !== '';
			},
			handleClick15(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay15 = '1）A级检修时\n2）必要时';
			  } else if (item.name === '判据') {
			    this.textToDisplay15 = '1）阻抗和功率损耗值在相同试验条件下与历年数值比较,不应有显著变化；\n2）出现以下变化时应注意：\na）交流阻抗值与出厂数据或历史数据比较,减小超过10%;\nb）损耗与出厂数据或历史数据比较,增加超过10%；\nc）当交流阻抗与出厂数据或历史数据比较减小超过8%,同时损耗与出厂数据或历史数据比较增加超过8%；\nd）在转子升速与降速过程中，相邻转速下，相同电压的交流阻抗或损耗值发生5%以上的突变时。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay15 = '1）隐极式转子在膛外或膛内以及不同转速下 测量，显极式转子对每一个磁极绕组测量；\n2）每次试验应在相同条件、相同电压下进行，试验电压参考出厂试验和交接试验电压值，但峰值不超过额定励磁电压；\n3）本试验可用动态匝间短路监测法或极平衡法试验代替；\n4）与历年数值比较，如果变化较大可采用动态匝间短路监测法、重复脉冲法等方法查明转子绕组是否存在匝间短路；\n5）测量转速按照DL/T 1525,转速间隔300r/min。';
			  } else {
			    this.textToDisplay15 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay15 !== '';
			},
			handleClick16(item) {
			  console.log('item', item);
			  if (item.name === '周期') {
			    this.textToDisplay16 = '必要时';
			  } else if (item.name === '判据') {
			    this.textToDisplay16 = '评定准则按照DL/T 1525。';
			  } else if (item.name === '方法及说明') {
				this.textToDisplay16 = '试验条件、设备及方法按照DL/T 1525。';
			  } else {
			    this.textToDisplay16 = '加载错误，请重试';
			  }
			  this.showText = this.textToDisplay16 !== '';
			},
		}
	}
</script>
<style scoped
	lang="scss">
	.header {
		padding: 30rpx;
		font-size: 30rpx;
		color: #333;
	}
	.item {
		padding: 10rpx 10rpx;
		&-title {
			.text {
				font-weight: 700;
				font-size: 33rpx;
				color: #111;
			}
		}
		&-content {
			padding: 0rpx 0;
			
		}
	}
	.gap {
		padding: 0 30rpx;
	}
	
	.txt {
		font-size: 34rpx;
		color: #111;
		
	}
</style>