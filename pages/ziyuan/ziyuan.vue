<template>
	<view>
		<uv-notice-bar :text="listtxt1" mode="closable" bgColor="#fef0f0" color="#e45656"></uv-notice-bar>
		<uv-index-list :index-list="indexList" customNavHeight="100rpx">
			<!-- <template v-slot:header>
				<view style="height: 100rpx;width: 750rpx;background-color: #3c9cff;">头部内容</view>
			</template> -->
			<template v-for="(item, index) in itemArr">
				<!-- #ifdef APP-NVUE -->
				<uv-index-anchor :text="indexList[index]"></uv-index-anchor>
				<!-- #endif -->
				<uv-index-item>
					<!-- #ifndef APP-NVUE -->
					<uv-index-anchor :text="indexList[index]"></uv-index-anchor>
					<!-- #endif -->
					<view class="list-cell" v-for="(cell, cellIndex) in item" :key="cellIndex">
						<view class="cell-content">
							<view class="cell-title">
								{{ cell }}
							</view>
							<view class="cell-description">
								{{ getDescription(cell) }}
							</view>
						</view>
						<view class="cell-actions">
							<view class="action-button" @click="navigateTo(cell)">预览</view>
							<view class="action-button" @click="download(cell)">下载</view>
						</view>
					</view>
				</uv-index-item>
			</template>
		</uv-index-list>
	</view>
</template>

<script>
import { shareMixin } from '/shareMixin.js';    //分享小程序的js引入
export default {
  mixins: [shareMixin],
  data() {
    return {
      listtxt1: '本页面内所有标准均取自互联网，仅供学习，请勿商用！如有需要的标准文件可联系我增加，有问题请联系QQ/WX：453555098',
      indexList: ["★", "B", "F", "J","M", "S"],
      itemArr: [
        ['电力设备预防性试验规程', '电气装置安装工程电气设备交接试验标准', '输变电设备状态检修试验规程', '电力安全工器具预防性试验'],
        ['干式电力变压器技术参数和要求', '电力变压器 第3部分 绝缘水平、绝缘试验和外绝缘空气间隙', '电力变压器 第6部分：电抗器','电力变压器 第10部分：声级测定','电力变压器 第11部分：干式变压器','变压器油中溶解气体分析和判断导则'],
        ['隐极同步发电机技术要求', '隐极同步发电机转子匝间短路故障诊断导则', '隐极式同步发电机转子匝间短路测定方法','隐极同步发电机定子绕组端部动态特性和振动测量方法及评定','发电机定子铁心磁化试验导则2016','发电机定子铁心磁化试验导则2024','发电机定子绕组端部电晕检测与评定导则'],
        ['介质损耗因数tanδ试验',],
		['金属封闭母线',],
		['输变电设备绝缘配合', ]
      ]
    }
  },
  methods: {
    getDescription(cell) {        //   标准对应的标准标号
      const descriptions = {
        '电力设备预防性试验规程': 'DL/T 596-2021',
        '电气装置安装工程电气设备交接试验标准': 'GB 50150-2016',
        '输变电设备状态检修试验规程': 'DL/T 393-2010',
		'电力安全工器具预防性试验':'DL/T 1476-2023',
        '干式电力变压器技术参数和要求': 'GB/T 10228-2023',
        '电力变压器 第3部分 绝缘水平、绝缘试验和外绝缘空气间隙': 'GB/T 1094.3-2017',
        '电力变压器 第6部分：电抗器': 'GB/T 1094.6-2011',
		'电力变压器 第10部分：声级测定':'GB/T 1094.10-202',
		'电力变压器 第11部分：干式变压器':'GB/T 1094.11-2022',
		'变压器油中溶解气体分析和判断导则':'DL/T 722-2014',
        '隐极同步发电机技术要求': 'GB/T 7064-2017',
        '隐极同步发电机转子匝间短路故障诊断导则': 'DL/T 1525-2016',
		'隐极式同步发电机转子匝间短路测定方法':'JB/T 8446-2013',
        '隐极同步发电机定子绕组端部动态特性和振动测量方法及评定': 'GB/T 20140-2016',
		'发电机定子铁心磁化试验导则2016':'GB/T 20835-2016',
		'发电机定子铁心磁化试验导则2024':'GB/T 20835-2024',
		'发电机定子绕组端部电晕检测与评定导则':'DL/T 298-2011',
		'介质损耗因数tanδ试验':'DL/T 474.3-2018',
		'金属封闭母线':'GB/T 8349-2000',
        '输变电设备绝缘配合': 'GB 311.1-2012',
        '列表S2': '222g',
        '列表S3': '333g'
      };
      return descriptions[cell] || '';
    },
    navigateTo(cell) {
      let path = '';
      switch (cell) {
        case '电力设备预防性试验规程':
          path = '/pages/preview/preview';
          // 传递预览网址，可以根据实际情况修改链接
          const previewUrl1 = 'https://mp.weixin.qq.com/s/2WpU0qG5HduW5kNY1q_i1w'; // 请替换为实际的预览网址
            uni.navigateTo({
              url: `${path}?url=${encodeURIComponent(previewUrl1)}`
              });
          break;
        case '电气装置安装工程电气设备交接试验标准':
          path = '/pages/preview/preview';
          // 传递预览网址，可以根据实际情况修改链接
          const previewUrl2 = 'https://mp.weixin.qq.com/s/RtZzklxaYYttVIdipUywUg'; // 替换为实际的预览网址
            uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl2)}`
                });
		  break;
        case '输变电设备状态检修试验规程':
          path = '/pages/preview/preview';
          // 传递预览网址，可以根据实际情况修改链接
          const previewUrl3 = 'https://mp.weixin.qq.com/s/z5Lkg9fzbRbUFR_oTr5I7Q'; // 替换为实际的预览网址
            uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl3)}`
                });
          break;
		case '电力安全工器具预防性试验':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl4 = 'https://mp.weixin.qq.com/s/TBsCmmYVPD7cDqKfKx22_A'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl4)}`
		        });
		  break;
        case '干式电力变压器技术参数和要求':
          path = '/pages/preview/preview';
            // 传递预览网址，可以根据实际情况修改链接
          const previewUrl5 = 'https://mp.weixin.qq.com/s/TBsCmmYVPD7cDqKfKx22_A'; // 替换为实际的预览网址
              uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl5)}`
                });
          break;
        case '电力变压器 第3部分 绝缘水平、绝缘试验和外绝缘空气间隙':
          path = '/pages/preview/preview';
            // 传递预览网址，可以根据实际情况修改链接
          const previewUrl6 = 'https://mp.weixin.qq.com/s/FzZ2_jBArnIRSI3q9r6VYg'; // 替换为实际的预览网址
              uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl6)}`
                });
          break;
        case '电力变压器 第6部分：电抗器':
          path = '/pages/preview/preview';
            // 传递预览网址，可以根据实际情况修改链接
          const previewUrl7 = 'https://mp.weixin.qq.com/s/Ke0Tl_G1QPcZwMf0VNC-9Q'; // 替换为实际的预览网址
              uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl7)}`
                });
          break;
		case '电力变压器 第10部分：声级测定':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl8 = 'https://mp.weixin.qq.com/s/PoOG_NsiU8sAxAVRZUc-7w'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl8)}`
		        });
		  break;
		case '电力变压器 第11部分：干式变压器':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl9 = 'https://mp.weixin.qq.com/s/DyPKwRQcLHr-Rtrg-_F-2Q'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl9)}`
		        });
		  break;
		
		case '变压器油中溶解气体分析和判断导则':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl16 = 'https://mp.weixin.qq.com/s/I9CK_g6ayJiSQDCnl7tQvg'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl16)}`
		        });
		  break;
        case '隐极同步发电机技术要求':
          path = '/pages/preview/preview';
            // 传递预览网址，可以根据实际情况修改链接
          const previewUrl10 = 'https://mp.weixin.qq.com/s/5yU8uhszMpDK4dURmUyYSA'; // 替换为实际的预览网址
              uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl10)}`
                });
          break;
        case '隐极同步发电机转子匝间短路故障诊断导则':
          path = '/pages/preview/preview';
            // 传递预览网址，可以根据实际情况修改链接
          const previewUrl11 = 'https://mp.weixin.qq.com/s/5tPHeuPtjQTfB_r8pdRsmQ'; // 替换为实际的预览网址
              uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl11)}`
                });
          break;
		case '隐极式同步发电机转子匝间短路测定方法':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl15 = 'https://mp.weixin.qq.com/s/I9CK_g6ayJiSQDCnl7tQvg'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl15)}`
		        });
		  break;
        case '隐极同步发电机定子绕组端部动态特性和振动测量方法及评定':
          path = '/pages/preview/preview';
            // 传递预览网址，可以根据实际情况修改链接
          const previewUrl12 = 'https://mp.weixin.qq.com/s/Bwak-xOTV-DHjIIu43pOYw'; // 替换为实际的预览网址
              uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl12)}`
                });
          break;
		case '发电机定子铁心磁化试验导则2016':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl13 = 'https://mp.weixin.qq.com/s/Uknh6hdNxcbkmx2dNX3J8g'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl13)}`
		        });
		  break;
		case '发电机定子铁心磁化试验导则2024':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl14 = 'https://mp.weixin.qq.com/s/J9TbW13rGi4nSnBEriVRnw'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl14)}`
		        });
		  break;
		case '发电机定子绕组端部电晕检测与评定导则':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl18 = 'https://mp.weixin.qq.com/s/5Tn9M2Ll5H7-DSUNbMWsKA'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl18)}`
		        });
		  break;
		case '介质损耗因数tanδ试验':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl19 = 'https://mp.weixin.qq.com/s/dd-1dvOi4wxpAqUjQt6xpg'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl19)}`
		        });
		  break;
		case '金属封闭母线':
		  path = '/pages/preview/preview';
		    // 传递预览网址，可以根据实际情况修改链接
		  const previewUrl17 = 'https://mp.weixin.qq.com/s/eJ-_K2umCJdSlsJtR6zsMA'; // 替换为实际的预览网址
		      uni.navigateTo({
		        url: `${path}?url=${encodeURIComponent(previewUrl17)}`
		        });
		  break;
        case '输变电设备绝缘配合':
          path = '/pages/preview/preview';
            // 传递预览网址，可以根据实际情况修改链接
          const previewUrl20 = 'https://mp.weixin.qq.com/s/QVmIwBCvmaaEAIVah4kk1g'; // 替换为实际的预览网址
              uni.navigateTo({
                url: `${path}?url=${encodeURIComponent(previewUrl20)}`
                });
          break;
		  
        default:
          path = '/';
      }
      if (path !== '/pages/preview/preview') {
        uni.navigateTo({
          url: path
        });
      }
    },
    download(cell) {
      let path = '';
      switch (cell) {
        case '电力设备预防性试验规程':
          path = 'https://p.huanvip.cn/down.php/45742b8363224b74ff4f65db098659e8.pdf';
          break;
        case '电气装置安装工程电气设备交接试验标准':
          path = 'https://p.huanvip.cn/down.php/8fd7893e0496a9fe799a2e27d658eef0.pdf';
          break;
        case '输变电设备状态检修试验规程':
          path = 'https://p.huanvip.cn/down.php/fd502e05ba8823d8057e1326c31c6c6b.pdf';
          break;
		case '电力安全工器具预防性试验':
		  path = 'https://p.huanvip.cn/down.php/37a498be2ca9f870530875f59f086a9a.pdf';
		  break;
        case '干式电力变压器技术参数和要求':
          path = 'https://p.huanvip.cn/down.php/47fb6e6319f91309b5a88c2049ec9780.pdf';
          break;
        case '电力变压器 第3部分 绝缘水平、绝缘试验和外绝缘空气间隙':
          path = 'https://p.huanvip.cn/down.php/64ee4cb135a6a8197a550f9cd34422e7.pdf';
          break;
        case '电力变压器 第6部分：电抗器':
          path = 'https://p.huanvip.cn/down.php/3e542744eda6f0c03130c768679e767e.pdf';
          break;  
		case '电力变压器 第10部分：声级测定':
		  path = 'https://p.huanvip.cn/down.php/98f37435bff6218a6109966b3f1047db.pdf';
		  break;  
		case '电力变压器 第11部分：干式变压器':
		  path = 'https://p.huanvip.cn/down.php/4238d7ab2b48f8a2fdefb1b351600578.pdf';
		  break;
		case '变压器油中溶解气体分析和判断导则':
		  path = 'https://p.huanvip.cn/down.php/d0aada44bff70262a7c43e274e423764.pdf';
		  break;
        case '隐极同步发电机技术要求':
          path = 'https://p.huanvip.cn/down.php/f46219f3f0cb0a77fb57345a0f6c447b.pdf';
          break;
        case '隐极同步发电机转子匝间短路故障诊断导则':
          path = 'https://p.huanvip.cn/down.php/e9168d0bead81aa0efc9a08b2bca7eb3.pdf';
          break;
		case '隐极式同步发电机转子匝间短路测定方法':
		  path = 'https://p.huanvip.cn/down.php/5f994ead033b0e2cf034fdf6c66feb4c.pdf';
		  break;
        case '隐极同步发电机定子绕组端部动态特性和振动测量方法及评定':
          path = 'https://p.huanvip.cn/down.php/c84527a0f5b64320d3862c856f963f3c.pdf';
          break;
		case '发电机定子铁心磁化试验导则2016':
		  path = 'https://p.huanvip.cn/down.php/c17a75b553b3a07684ac37f130fd97d4.pdf';
		  break;
		case '发电机定子铁心磁化试验导则2024':
		  path = 'https://p.huanvip.cn/down.php/696762b815385befbad487bdfac5661d.pdf';
		  break;
		case '发电机定子绕组端部电晕检测与评定导则':
		  path = 'https://p.huanvip.cn/down.php/c488ba8a372b21515aa4864e111f490e.pdf';
		  break;
		case '介质损耗因数tanδ试验':
		  path = 'https://p.huanvip.cn/down.php/96e052385d481603be6eae1d0e674429.pdf';
		  break;
		case '金属封闭母线':
		  path = 'https://p.huanvip.cn/down.php/32d6d6235c4c41dd1206c9dae4a63c13.pdf';
		  break;
        case '输变电设备绝缘配合':
          path = 'https://p.huanvip.cn/down.php/6577b2befe28067edf018065c0c0f574.pdf';
          break;
		  
        default:
          path = '/';
      }
      // 复制链接
      uni.setClipboardData({
        data: path,
        success: () => {
          uni.showToast({
            title: '链接已复制\n请打开浏览器下载',
            icon: 'success',
			duration: 2000
          });
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.list-cell {
	display: flex;
	flex-direction: row; /* 水平排列 */
	box-sizing: border-box;
	width: 100%;
	padding: 10px 24rpx;
	overflow: hidden;
	color: #323233;
	font-size: 14px;
	line-height: 24px;
	background-color: #fff;
	border-bottom: 1px solid #e0e0e0; /* 添加灰色分割线 */
}

.cell-content {
	flex: 1; /* 内容区域占据剩余空间 */
	display: flex;
	flex-direction: column;
	justify-content: center; /* 垂直居中 */
}

.cell-title {
	font-weight: bold;
}

.cell-description {
	font-size: 14px;
	color: #888;
}

.cell-actions {
	display: flex;
	flex-direction: row;
	align-items: center; /* 垂直居中 */
}

.action-button {
	margin-left: -10rpx; /* 预览按钮与下载按钮之间的间距 */
	margin-right: 20rpx; /* 下载按钮右边的边距 */
	text-decoration: underline;
	color: #007AFF; /* 仿超链接的颜色 */
	cursor: pointer;
	font-size: 14px;
}

.action-button:hover {
	color: #0056b3; /* 悬停时的颜色 */
}
</style>