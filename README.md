
# 更新记录
## 1.0.0（2020-03-16）
九宫格抽奖，可自定义速度和抽奖位置
# 简介
九宫格抽奖，可自定义速度、抽奖位置。
<!-- # [gitlab地址](https://git.lug.ustc.edu.cn/LiYaMei94/jiugongge_lottery)-->
<!-- # [演示地址](https://git.lug.ustc.edu.cn/LiYaMei94/jiugongge_lottery) -->
# SJ-LotteryDraw
## SJ-LotteryDraw组件参数说明
|参数| 类型 |默认值
|--|--|--|
| grid_info_arr | Array |[{logo:"",text:""}]（详细信息如下所示）
| lottery_draw_param | Object |{logo:"",text:""}（详细信息如下所示）
### grid_info_arr详情

```javascript
grid_info_arr:[
	{
		logo:"../../static/SJ-LotteryDraw/grid_img_1.png",//每个格子显示的图片
		text:"手机"//每个格子的文字（奖品名称）
	},
	{
		logo:"../../static/SJ-LotteryDraw/grid_img_1.png",
		text:"零食包"
	},
	{
		logo:"../../static/SJ-LotteryDraw/grid_img_1.png",
		text:"口红"
	},
	{
		logo:"../../static/SJ-LotteryDraw/grid_img_1.png",
		text:"谢谢参与"
	},
	{
		logo:"../../static/SJ-LotteryDraw/grid_img_1.png",
		text:"压缩饼干"
	},
	{
		logo:"../../static/SJ-LotteryDraw/grid_img_1.png",
		text:"水杯"
	},
	{
		logo:"../../static/images/grid_img_1.png",
		text:"QQ糖"
	},
	{
		logo:"../../static/images/grid_img_1.png",
		text:"耳机"
	},
	{
		logo:"../../static/images/grid_img_1.png",
		text:"谢谢参与"
	},
]
```
### lottery_draw_param 详情

```javascript
lottery_draw_param:{
	startIndex: 0, //开始抽奖位置，从0开始
	totalCount: 4, //一共要转的圈数
	winingIndex: 2, //中奖的位置，从0开始
	speed: 50,//抽奖动画的速度 [数字越大越慢,默认100]
	domData:grid_info_arr//长度为九的数组
}
```
## SJ-LotteryDraw组件事件说明

```javascript
luck_draw_finish(param);//抽奖完成时触发，返回抽奖停留的格子信息
```

## scss文件参数

```css
$grid_wrap_bg: #9ad3ff; //九宫格背景色(包括边框色)
$grid_wrap_inner_bg: #61a2fc; //九宫格内层背景色
$grid_wrap_shadow: #89bbf7; //九宫格外层下边框阴影色

// 边框
$grid_bobble_bg: #bce0e9; //边框小球颜色
$grid_Bigball_bg: #f5fbc8; //边框大球颜色

// 除了抽奖按钮外的格子样色变量
$grid_item_color: #708abf; //每个格子的字体颜色
$grid_item_bg: #ffffff; //每个格子的背景颜色
$grid_item_bg_shadow: #9cd2ff; //每个格子的下边阴影颜色

// 抽奖按钮格子,活动格子颜色变量
$grid_play_btn_bg: #ff3a59; //抽奖按钮背景色
$grid_play_btn_color: #ffffff; //抽奖按钮字体色
$grid_play_btn_shadow: #ea0125; //抽奖按钮下边框阴影色

$grid_wrap_width: 530upx; //九宫格宽度(包括边框)
$grid_wrap_height: 530upx; //九宫格高度
$grid_wrap_shadowSize: 12upx; //格子的阴影大小

$grid_wrap_inner_width: 460upx; //九宫格内层的宽度(不包括边框)
$grid_wrap_inner_height: 460upx; //九宫格内层的高度

$grid_item_margin: 20upx; //格子与格子，格子与边框之间的距离
$grid_item_shadowSize: 8upx; //格子的阴影大小
$grid_item_fontSize:20upx;//格子字体大小
$grid_play_btn_fontSize: 40upx; //抽奖按钮字体大小

$grid_border_size: ($grid_wrap_width - $grid_wrap_inner_width)/2; //边框的大小（外层宽-内层宽）/2

$grid_item_width: ($grid_wrap_inner_width - $grid_item_margin * 4)/3; //每个格子的宽度(内层宽-格子间距*4)/3
$grid_item_height: ($grid_wrap_inner_width - $grid_item_margin * 4)/3; //每个格子的高度(内层高-格子间距*4)/3

$grid_item_logo_width: 70upx; //每个格子内的图片宽度
$grid_item_logo_height: 70upx; //每个格子内的图片高度度

$grid_bobble_size: 17upx; //边框小球大小
$grid_Bigball_size: 24upx; //边框大球大小
$grid_Ball_margin: 10upx; //球与球之间的距离
```

## 使用方式

```javascript
<template>
	<view class="content">
		<LotteryDraw @get_winingIndex='get_winingIndex' :lottery_draw_param='lottery_draw_param' @luck_draw_finish='luck_draw_finish'></LotteryDraw>
	</view>
</template>

<script>
import LotteryDraw from '../../components/SJ-LotteryDraw/SJ-LotteryDraw.vue';
export default {
	components:{
		LotteryDraw
	},
	data() {
		return {
			
			lottery_draw_param:{
				startIndex: 0, //开始抽奖位置，从0开始
				totalCount: 4, //一共要转的圈数
				winingIndex: 4, //中奖的位置，从0开始
				speed: 50 //抽奖动画的速度 [数字越大越慢,默认100]
			}
		};
	},
	onLoad() {
		
	},
	methods: {
		// 修改获奖位置（可以在这里获取后台的数据
		get_winingIndex(callback){
			this.lottery_draw_param.winingIndex=7;
			callback();
		},
		// 抽奖完成
		luck_draw_finish(param){
			
			console.log(param)
			// console.log(`抽到第${param+1}个方格的奖品`)
		}
		
	}
};
</script>

<style scoped>
.content {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

</style>


```
# 适应PC端
新建一个js文件，文件内容如下所示，然后在main.js文件中引入即可使用。
```javascript
(function (){
	var u = navigator.userAgent,
		w = window.innerWidth;
	if (!u.match(/AppleWebKit.*Mobile.*/) || u.indexOf('iPad') > -1) {
		var sw = w*576/1920;
		window.innerWidth = sw<375?375:sw;
                window.onload = function() {
		        window.innerWidth = w;
	        }
	}
})();
```

```javascript
import pc from './utils/pc.js'
import Vue from 'vue'
import App from './App'

Vue.config.productionTip = false

App.mpType = 'app'

const app = new Vue({
    ...App
})
app.$mount()

```

# 注意：
- 在运行到小程序开发工具时请把main.js中的import pc from './utils/pc.js'注释掉
