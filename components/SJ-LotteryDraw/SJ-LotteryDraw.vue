<template>
	<view class="lottery_container">
		<view class="grid_wrap">
			<view class="lottery_wrap">
				<ul class="lottery_grid">
					<li v-for="(item, index) in grid_info_arr" :class="{ active: current_index == index && index != 8 }" :key="index" @click="luck_draw" :data-index="index">
						<image v-if="index != 8" class="grid_img" mode='aspectFit' :src="item.logo" alt="">
						{{ index == 8 ? '抽奖' : index+1 }}
					</li>
				</ul>
			</view>
			<view class="lottery_wrap_border">
				<ul v-for="(item, index) in 4" :key="index">
					<li v-for="(item, index) in 12" :key="index"></li>
				</ul>
			</view>
		</view>
		<!-- 抽奖完成弹出的窗口 -->
		<!-- <view class="lottery_finish_wrap">
			
		</view> -->
	</view>
	
</template>

<script>
import LotteryDraw from './SJ-LotteryDraw.js';
let grid_info=[
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"手机"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"零食包"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"口红"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"谢谢参与"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"压缩饼干"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"水杯"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"QQ糖"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"耳机"
				},
				{
					logo:"../../static/SJ-LotteryDraw/SJ-LotteryDraw.png",
					text:"谢谢参与"
				},
			];
export default {
	data() {
		return {
			current_index: -1,
		};
	},
	props:{
		grid_info_arr:{
			type:Array,
			default:function () {
				return grid_info
			}
		},
		lottery_draw_param:{
			type:Object,
			default:function () {
				return {
						startIndex: 0, //开始抽奖位置，从0开始
						totalCount: 4, //一共要转的圈数
						winingIndex: 2, //中奖的位置，从0开始
						speed: 50 //抽奖动画的速度 [数字越大越慢,默认100]
					}
			}
		},
		
	},
	onLoad() {
		console.log(this.lottery_draw_param)
	},
	
	methods: {
		luck_draw(event) {
			let index = event.currentTarget.dataset.index;
			if (index == 8) {
				
				// 在这里拿到停止的位置,然后修改父组件中lottery_draw_param的值
				this.$emit('get_winingIndex',6);
				console.log(this.lottery_draw_param)
				
				let that = this;
				let win = new LotteryDraw({
					domData:that.grid_info_arr,
					...that.lottery_draw_param
				},
					function(index,count) {
						that.current_index = index;
						if(that.lottery_draw_param.winingIndex==index&&that.lottery_draw_param.totalCount==count){
							that.$emit('luck_draw_finish',that.grid_info_arr[index])
							// console.log('抽到了')
						}
					}
				);
			}
		}
	}
};
</script>

<style scoped lang="css">
@import './SJ-LotteryDraw.css';
</style>
