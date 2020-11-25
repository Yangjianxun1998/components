<template>
	<view id="number">
		<view class="numbox">
			<view @click="delnum" v-if="numvalue > 0" class="iconfont icon-jianhao"></view>
			<view class="numbox_title" v-if="numvalue > 0">{{ numvalue }}</view>
			<view v-if="max > numvalue" @click="addnum" class="iconfont icon-jiahao"></view>
			<view v-if="max <= numvalue" @click="titlrget" class="iconfont icon-jiahao serite"></view>
		</view>
	</view>
</template>

<script>
export default {
	props: {
		max:{
			type: [Number, String],
			default: 10
		}
	},
	data() {
		return {
			numvalue: 0,
		};
	},
	methods: {
		delnum() {
			this.numvalue = this.numvalue - 1;
			this.$emit('change', this.numvalue);
		},
		addnum() {
			this.numvalue = this.numvalue + 1;
			this.$emit('change', this.numvalue);
		},
		titlrget(){
			this.until.remind('抱歉,超出商品可购范围！')
		}
	}
};
</script>

<style lang="less" scoped>
view {
	.numbox {
		display: flex;
		.iconfont {
			font-size: 40rpx;
		}
		.numbox_title {
			font-size: 30rpx;
			width: 50rpx;
			height: 40rpx;
			line-height: 40rpx;
			text-align: center;
			color: #2f3f50;
		}
		.icon-jianhao {
			color: #c9cdd8;
		}
		.icon-jiahao {
			color: #c7000a;
		}
		.serite{
			color: #ececec;
		}
	}
}
</style>
