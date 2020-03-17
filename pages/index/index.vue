<template>
	<view class="content">
		<LotteryDraw @luck_draw_finish='luck_draw_finish'></LotteryDraw>
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
			
		};
	},
	onLoad() {
	},
	methods: {
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
